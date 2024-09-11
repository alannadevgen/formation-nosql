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

