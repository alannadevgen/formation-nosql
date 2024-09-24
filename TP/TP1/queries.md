# Séance 1 - Introduction à MongoDB

1. Donner les styles de cuisine présent dans la collection
```python
db.restaurants.distinct(key="cuisine")
```
2. Donner tous les grades possibles dans la base
```python
db.restaurants.distinct("grades.grade")
```
3. Compter le nombre de restaurants proposant de la cuisine française ("French")
```python
db.restaurants.count_documents({ "cuisine": "French" })
```
4. Compter le nombre de restaurants situés sur la rue "Central Avenue"
```python
db.restaurants.count_documents({ "address.street": "Central Avenue" })
```
5. Compter le nombre de restaurants ayant eu une note supérieure à 50
```python
db.restaurants.count_documents({
    "grades.score": { "$gt": 50 }
})
```
6. Lister tous les restaurants, en n'affichant que le nom, l'immeuble et la rue
```python
addresses = db.restaurants.find(
    {},
    { "_id": 0 , "name": 1, "address.building": 1, 
  "address.street": 1 }
)
pandas.DataFrame(list(addresses))
```
7. Lister tous les restaurants nommés "Burger King" (nom et quartier uniquement)
```python
bk = db.restaurants.find(
    { "name": "Burger King" },
    { "_id": 0, "name": 1, "borough": 1 }
)
pandas.DataFrame(list(bk))
```
8. Lister les restaurants situés sur les rues "Union Street" ou "Union Square"
```python
union_street_square = db.restaurants.find(
    { "address.street": { "$in": [ "Union Street", "Union Square" ] }},
    { "_id": 0, "name": 1, "borough" : 1 }
)
pandas.DataFrame(list(union_street_square))
```
9. Lister les restaurants situés au-dessus de la lattitude 40.90
```python
lat40_90 = db.restaurants.find(
    { "address.coord.1": { "$gt": 40.9 }},
    { "_id": 0, "name": 1, "borough": 1, "address.coord": 1 }
)
pandas.DataFrame(list(lat40_90))
```
10. Lister les restaurants ayant eu un score de 0 et un grade "A"
```python
score0_gradeA = db.restaurants.find(
    { "grades.score": 0, "grades.grade": "A" },
    { "_id": 0, "name": 1, "borough": 1, "grades": 1 }
)
pandas.DataFrame(list(score0_gradeA))
```