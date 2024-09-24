# Séance 2 - Agrégation avec MongoDB

1. Quelles sont les 10 plus grandes chaînes de restaurants (i.e les restaurants avec un nom identique) ? Il existe deux façons de faire.
```python
top10 = db.restaurants.aggregate([
    { "$match": { "name": { "$ne": "" }}},
    { "$sortByCount": "$name"},
    { "$limit": 10}
])
pandas.DataFrame(list(top10))
```
2. Donner le Top 5 et le Flop 5 des types de cuisine, en terme de nombre de restaurants. Il faut faire 2 requêtes.

Top 5
```python
top5 = db.restaurants.aggregate([
    { "$group": { "_id": "$cuisine", "nb": { "$sum": 1 }}},
    { "$sort": { "nb": -1 }},
    { "$limit": 5}
])
pandas.DataFrame(list(top5))
```
Flop 5
```python
flop5 = db.restaurants.aggregate([
    { "$group": { "_id": "$cuisine", "nb": { "$sum": 1 }}},
    { "$sort": { "nb": 1 }},
    { "$limit": 5}
])
pandas.DataFrame(list(flop5))
```
3. Quelles sont les 10 rues avec le plus de restaurants ?
```python
top10_address = db.restaurants.aggregate([
    { "$sortByCount": "$address.street" },
    { "$limit": 10 }
])
pandas.DataFrame(list(top10_address))
```
4. Quelles sont les rues situées sur strictement plus de 2 quartiers ? Essayez d'ajouter le nom des quartiers de chaque rue (cf `addToSet`).
```python
two_boroughs = db.restaurants.aggregate([
    { "$group": {
        "_id": "$address.street",
        "quartiers": { "$addToSet": "$borough" }
    }},
    { "$addFields": { "nb_quartier": { "$size": "$quartiers"}}},
    { "$sort": { "nb_quartier": -1 }},
    { "$match": { "nb_quartier": { "$gt": 2 }}}
])
pandas.DataFrame(list(two_boroughs))
```
5. Lister par quartier le nombre de restaurants et le score moyen. Attention à bien découper le tableau `grades`

Pour cette question il existe plusieurs façons de faire. Voici une proposition.

**Version 1** : score moyen de la dernière visite
```python
borough_nb_rest_avg_score = db.restaurants.aggregate([
    { "$addFields": {
        "first_grade": { "$first": "$grades" }
    }},
    { "$group": {
        "_id": "$borough",
        "nb_restaurants": { "$sum": 1 },
        "score_moyen": { "$avg": "$first_grade.score" }
    }},
    { "$sort": { "score_moyen": 1 }}
])
pandas.DataFrame(list(borough_nb_rest_avg_score)).round(2)
```
**Version 2** : score moyen de toutes les visites
```python
borough_nb_rest_avg_score = db.restaurants.aggregate([
    { "$unwind": "$grades" },
    { "$group": {
        "_id": { "id_resto": "$_id", "br": "$borough" },
        "nb_visites": { "$sum": 1 },
        "score_tot": { "$sum": "$grades.score" }
    }},
    { "$group": {
        "_id": "$_id.br",
        "nb_restaurants": { "$sum": 1 },
        "nb_visites": { "$sum": "$nb_visites" },
        "score_total": { "$sum": "$score_tot" }
    }},
    { "$addFields": {
        "score_moyen": {
            "$divide": [ "$score_total", "$nb_visites" ]
                       }
    }},
    { "$sort": { "score_moyen": 1 }}
])
pandas.DataFrame(list(borough_nb_rest_avg_score)).round(2)
```
**Version 3** : score moyen de la dernière visite
```python
borough_nb_rest_avg_score = db.restaurants.aggregate([
    { "$unwind": "$grades" },
    { "$group": {
        "_id": "$borough",
        "liste_restaurants": { "$addToSet": "$_id" },
        "score_moyen": { "$avg": "$grades.score" }
    }},
    { "$addFields": {
        "nb_resto": { "$size": "$liste_restaurants" }
    }},
    { "$sort": { "score_moyen": 1 }}
])
pandas.DataFrame(list(borough_nb_rest_avg_score)).round(2)
```
6. Donner les dates de début et de fin des évaluations
```python
start_end_dates = db.restaurants.aggregate([
    { "$unwind": "$grades" },
    { "$group": {
        "_id": "Tous",
        "deb": { "$min": "$grades.date" },
        "fin": { "$max": "$grades.date" }
    }}
])
pandas.DataFrame(list(start_end_dates))
```
7. Quels sont les 10 restaurants (nom, quartier, addresse et score) avec le plus petit score moyen ?
```python
min_avg_score = db.restaurants.aggregate([
    { "$unwind": "$grades" },
    { "$match": { "grades.score": { "$gte": 0 }}},
    { "$group": {
        "_id": { "n": "$name", "b": "$borough", "a": "$address" },
        "score": { "$avg": "$grades.score" },
        "nb_grades": { "$sum": 1 }
    }},
    { "$sort": { "score": 1, "nb_grades": -1 }},
    { "$limit": 10 },
    { "$project": {
        "Nom": "$_id.n", "Quartier": "$_id.q",
        "Adresse": "$_id.a", "score": 1, "_id": 0,
        "nb_grades": 1
    }}
])
pandas.DataFrame(list(min_avg_score))
```

[//]: # (8. Quels sont les restaurants &#40;nom, quartier et addresse&#41; avec uniquement des grades "A" ?)

[//]: # (    - restriction à ceux qui ont A, découpage, suppression des autres grades que "A" et affichage des infos)

[//]: # (    - on peut envisager d'autres choses &#40;découpage, `addToSet`, et restriction à ceux pour lequel le tableau créé = ["A"] - par exemple&#41;)

[//]: # (```python)

[//]: # ()
[//]: # (```)

[//]: # (9. Compter le nombre d'évaluation par jour de la semaine.)

[//]: # (    &rarr; Recherche sur l'extraction du jour de la semaine à partir d'une date à faire.)

[//]: # (```python)

[//]: # ()
[//]: # (```)

[//]: # (10. Donner les 3 types de cuisine les plus présents par quartier)

[//]: # (    - Piste de réflexion)

[//]: # (        1. double regroupement à prévoir)

[//]: # (        2. tri à prévoir)

[//]: # (        3. regroupement avec `push`)

[//]: # (        4. `slice` pour prendre une partie d'un tableau)

[//]: # (```python)

[//]: # ()
[//]: # (```)