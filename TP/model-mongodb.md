# Modèle des données MongoDB

Le principe de base de MongoDB repose sur la représentation des données qui sont modélisées sous la forme de `documents`.

- Stocké en *Binary JSON* (`BSON`).
- Documents similaires rassemblés dans des `collections` : au sein d'une base de données, il peut y avoir plusieurs collections.
- Pas de schéma des documents définis en amont (contrairement à une BD relationnel ou une BD NoSQL de type *Column*).
- Les documents peuvent n'avoir aucun point commun entre eux.
- Un document contient (généralement) l'ensemble des informations.
- Idéalement il n'y a pas (ou très peu) de jointure à faire.
- MongoDB respecte les propriétés **CP** dans le théorème *CAP*.
- Au niveau d'un document, les propriétés ACID sont généralement respectées.

## Format `JSON`

- Le format de données `JSON` a été créé en 2005 et signifie `JavaScript Object Notation`.
- C'est un format léger d'échange de données structurées.
- Le schéma des données n'est pas connu (contenu dans les données)
- Basé sur deux notions :
	- collection de couples clé/valeur
	- liste de valeurs ordonnées
- Structures possibles :
	- objet (couples clé/valeur) : `{"nom": "dupont", "prenom": "jeanne"}`
	- tableau (collection de valeurs) : `[1, 5, 10]`
	- une valeur dans un objet ou dans un tableau peut être elle-même un littéral
- Deux types atomiques (`string` et `number`) et trois constantes (`true`, `false`, `null`)

Vous pouvez valider la structure d'un JSON sur [jsonlint.com/](http://jsonlint.com/)

### Exemple de `JSON`

```json
{
    "address": {
        "building": "469",
        "coord": [
            -73.9617,
            40.6629
        ],
        "street": "Flatbush Avenue",
        "zipcode": "11225"
    },
    "borough": "Brooklyn",
    "cuisine": "Hamburgers",
    "grades": [
        {
            "date": "2014-12-30 01:00:00",
            "grade": "A",
            "score": 8
        },
        {
            "date": "2014-07-01 02:00:00",
            "grade": "B",
            "score": 23
        }
    ],
    "name": "Wendy'S",
    "restaurant_id": "30112340"
}
```

### Compléments

`BSON` : extension de `JSON`

- Quelques types supplémentaires (identifiant spécifique, binaire, date, ...)
- Distinction entier et réel

**Schéma dynamique**

- Documents variant très fortement entre eux, même dans une même collection
- On parle de **self-describing documents**
- Ajout très facile d'un nouvel élément pour un document, même si cet élément est inexistant pour les autres
- Pas de `ALTER TABLE` ou de redesign de la base

### Langage d'interrogation

- Il n'existe pas de SQL.
- Définition d'un langage propre
    - `find()` : pour tout ce qui est restriction et projection
    - `aggregate()` : pour tout ce qui est calcul de variable, d'aggrégats et de manipulations diverses
    - ...


