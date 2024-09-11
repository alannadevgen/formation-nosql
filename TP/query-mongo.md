# Requêtage avec MongoDB

Les données `JSON` sont similaires à un dictionnaire `Python`. Pour récupérer le premier document, nous utilisons la fonction `find()` de l'objet créé `m`.

```python
first_doc = db.collection_name.find(limit = 1)
```

L'objet retourné est un **curseur**, et non le résultat. Nous avons celui-ci lorsque nous utilisons `first_doc` dans une commande telle qu'une transformation en `list` par exemple. 

```python
list(first_doc)
```

Une fois le résultat retourné (un seul élément ici), le curseur ne renvoie plus rien.

```python
list(first_doc)
```

## Dénombrement

La fonction `count_documents({})` permet de dénombrer les documents présents dans la collection.

```python
db.collection_name.count_documents({})
```
La fonction `estimated_document_count()` permet d'estimer le nombre de documents, cela est particulièrement utile lorsque la base de données
est déployée sur plusieurs servers avec une grande quantité de données et qu'une estimation précise du volume de données n'est pas nécessaire.

```python
db.collection_name.estimated_document_count()
```

## Sélection de documents

Pour sélectionner les documents, nous allons utiliser le paramètre dans la fonction `count_documents()` (ainsi que dans les fonctions `distinct()` et `find()` que nous verrons plus tard).

- `{}` : tous les documents
- `{ "champs": valeur }` : documents ayant cette valeur pour ce champs
- `{ condition1, condition2 }` : documents remplissant la condition 1 **ET** la condition 2
- `"champs.sous_champs"` : permet d'accéder donc à un sous-champs d'un champs (que celui-ci soit un littéral ou un tableau)
- `{ "champs": { "$opérateur": expression }}` : utilisation d'opérateurs dans la recherche
    - `$in` : comparaison à un ensemble de valeurs
    - `$gt`, `$gte`, `$lt`, `$lte`, `$ne` : comparaison (resp. *greater than*, *greater than or equal*, *less than*, *less than or equal*, *not equal*)

### Comptage de certains documents

> [!TIP]
> Les requêtes ci-dessous sont des exemples de requêtes sur une base de données fictive `students` à propos des étudiants et des cours qu'ils suivent à l'université.

- Nombre d'étudiants de l'Université de Paris

```python
db.students.count_documents({ "university": "Université de Paris" })
```

- Nombre d'étudiants de l'Université de Paris ayant suivi le cours de NoSQL

```python
db.students.count_documents({ "university": "Université de Paris", "course": "NoSQL" })
```

-  Nombre d'étudiants de l'Université de Paris ayant suivi le cours de NoSQL ou de Python

```python
db.students.count_documents(
  { 
    "university": "Université de Paris", 
    "course": { "$in": ["NoSQL", "Python"]} 
  }
)
```

- Nombre d'étudiants qui vivent Boulevard des Capucines

```python
db.students.count_documents(
  { 
    "address.street": "Boulevard des Capucines"
  }
)
```

- Étudiants.es ayant eu une note moyenne de 10

```python
db.students.count_documents(
  { 
    "grades.average": 10
  }
)
```
Ici le champ `average` est inclus dans `grades` autrement dit, nous avons la structure de données suivante :
```json
{
    "grades" : [
      {
        "average" : 10,
        "min" : 8,
        "max" : 16,
      }
    ],
    "..." : "..."
}
```

- Étudiants.es ayant eu une note moyenne inférieure à 8

```python
db.students.count_documents(
  { 
    "grades.average":{ "$lte": 8 }
  }
)
```

### Valeurs distinctes

On peut aussi voir la liste des valeurs distinctes d'un attribut, avec la fonction `distinct()`.

- Nombre de cours différents enseignés dans toutes les universités

```python
db.collection_name.distinct(key = "course")
```

- Nombre de cours enseignés à l'Université de Paris

```python
db.collection_name.distinct(
  key = "course",
  query = { "university": "Université de Paris" }
)
```

### Restriction et Projection

- Fonction `find()` pour réaliser les *restrictions* et *projections*
- Plusieurs paramètres : 
    - Restriction (quels documents prendre) : même format que précédemment
    - Projection (quels champs afficher)
    - `limit` pour n'avoir que les $n$ premiers documents
    - `sort` pour effectuer un tri des documents
- PyMongo renvoit un curseur, qu'il faut donc gérer pour avoir le résultat
- Transformation en `DataFrame` (du module `pandas`)
  - Ce format n'est pas forcément idéal pour certains champs, notamment ceux imbriqués.

### Sélection de champs à afficher ou non

Dans la fonction `find()`, pour choisir les champs à afficher, le deuxième paramètre permet de faire une projection avec les critères suivants :

- sans précision, l'identifiant interne est toujours affiché (`_id`)
- `{ "champs": 1 }` : champs à afficher
- `{ "champs": 0 }` : champs à ne pas afficher
- Pas de mélange des 2 sauf pour l'identifiant interne à MongoDB (`_id`)
    - `{ "_id": 0, "champs": 1, ...}`

### Tri et limites

Toujours dans la fonction `find()`, il est possible de faire le tri des documents, avec le paramètre `sort` qui prend un tuple composé d'un ou plusieurs tuples indiquant les critères de tri.

- `( "champs", 1 )` : tri croissant
- `( "champs", -1 )` : tri décroissant
- plusieurs critères de tri possibles (dans les 2 sens)

Dans ces fonctions, on peut aussi limiter l'exploration à une partie, avec les paramètres suivant :

- `limit` : restreint le nombre de résultats fournis
- `skip` : ne considère pas les *n* premiers documents

### Récupération des 5 premiers documents

Notez le contenu des colonnes `address` et `grades`.

```python
import pandas as pd
pd.DataFrame(list(db.collection_name.find(limit = 5)))
```

### Exemples

- Cours de NoSQL (uniquement les attributs `"name"` et `"surname"`)

```python
nosql_students = db.collection_name.find(
    { "course": "NoSQL" },
    { "student.name": 1, "student.surname": 1 }
)
pd.DataFrame(list(nosql_students))
```

- Idem sans l'identifiant interne

```python
nosql_students = db.collection_name.find(
    { "course": "NoSQL" },
    { "_id": 0, "student.name": 1, "student.surname": 1 }
)
pd.DataFrame(list(nosql_students))
```

- 5 meilleures notes de l'évaluation de NoSQL, supérieures à 15 (on affiche le nom et le prénom de l'étudiant)

```python
first_grades = db.collection_name.find(
    { "course": "NoSQL", "grades.score": { "$gte":  15}},
    { "_id": 0, "student.name": 1, "student.surname": 1 }
    limit = 5
)
pd.DataFrame(list(first_grades))
```

- Étudiants du cours de NoSQL, ayant une note supérieure à 12, trié par ordre décroissant des notes et ordre croissant du nom de famille (on affiche le nom et le prénom de l'étudiant).

```python
sorted = db.collection_name.find(
    { "course": "NoSQL", "grades.score": { "$gte":  12}},
    {"_id": 0, "student.name": 1, "student.surname": 1 },
    sort = (("grades.score", -1), ("student.surname", 1))
)
pd.DataFrame(list(c))
```
