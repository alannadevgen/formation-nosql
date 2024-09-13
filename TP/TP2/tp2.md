
# Agrégation avec MongoDB


## A faire

1. Quelles sont les 10 plus grandes chaines de restaurants (nom identique) ?
    - TOP 10 classique (2 façons de faire donc)
1. Donner le Top 5 et le Flop 5 des types de cuisine, en terme de nombre de restaurants
    - idem, avec le tri qui change entre les 2 demandes
1. Quelles sont les 10 rues avec le plus de restaurants ?
    - TOP 10 aussi
1. Quelles sont les rues situées sur strictement plus de 2 quartiers ?
    - Essayez d'ajouter le nom des quartiers de chaque rue (cf `addToSet`)
1. Lister par quartier le nombre de restaurants et le score moyen
    - Attention à bien découper le tableau `grades`
1. Donner les dates de début et de fin des évaluations
    - min et max sont dans un bateau
1. Quels sont les 10 restaurants (nom, quartier, addresse et score) avec le plus petit score moyen ?
    - découpage, regroupement par restaurant, tri et limite
1. Quels sont les restaurants (nom, quartier et addresse) avec uniquement des grades "A" ?
    - restriction à ceux qui ont A, découpage, suppression des autres grades que "A" et affichage des infos
    - on peut envisager d'autres choses (découpage, `addToSet`, et restriction à ceux pour lequel le tableau créé = ["A"] - par exemple)
1. Compter le nombre d'évaluation par jour de la semaine
    - petite recherche sur l'extraction du jour de la semaine à partir d'une date à faire
1. Donner les 3 types de cuisine les plus présents par quartier
    - simple à dire, compliqué à faire
    - une piste
        1. double regroupement à prévoir
        2. tri à prévoir
        3. regroupement avec `push`
        4. `slice` pour prendre une partie d'un tableau


## Données AirBnB

Nous allons travailler sur des données AirBnB. Celles-ci sont stockées sur le serveur Mongo dans la collection `listingsAndReviews` de la base `sample_airbnb`.

> [Aide sur les données](https://docs.atlas.mongodb.com/sample-data/sample-airbnb)

Une fois créée la connexion à la collection dans Python, répondre aux questions suivantes :

1. Lister les différentes types de logements possibles cf (`room_type`)
1. Lister les différents équipements possibles cf (`amenities`)
1. Donner le nombre de logements
1. Donner le nombre de logements de type "Entire home/apt"
1. Donner le nombre de logements proposant la "TV" et le "Wifi (cf `amenities`) 
1. Donner le nombre de logements n'ayant eu aucun avis
    - il existe les champs `number_of_reviews` et `reviews` (tableau des avis) - vérifiez qu'ils soient cohérents
1. Lister les informations du logement "10545725" (cf `_id`)
1. Lister le nom, la rue et le pays des logements dont le prix est supérieur à 10000
1. Donner le nombre de logements par type
1. Donner le nombre de logements par pays
1. On veut représenter graphiquement la distribution des prix, il nous faut donc récupérer uniquement les tarifs 
    - Un tarif apparraissant plusieurs fois dans la base doit être présent plusieurs fois dans cette liste
1. Calculer pour chaque type de logements (`room_type`) le prix (`price`)
1. On veut représenter la distribution du nombre d'avis. Il faut donc calculer pour chaque logement le nombre d'avis qu'il a eu (cf `reviews`)
1. Compter le nombre de logement pour chaque équipement possible
1. On souhaite connaître les 10 utilisateurs ayant fait le plus de commentaires