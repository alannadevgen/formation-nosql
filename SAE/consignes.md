# Consignes

## :car: Contexte

La directrice d'une entreprise de voitures, Paula DUPONT, veut opérer une migration depuis une base de données relationnelle vers une base de données NoSQL. En effet, la BDD actuelle commence à présenter des limites : requête avec forte latence, perte de données dues à des défaillances serveur (qui arrivent de plus en plus fréquement), etc.

Paula DUPONT vous missionne pour opérer la migration vers une base de données NoSQL. Pour cela elle vous met à disposition son jeu de données nommé `ClassicModel`.

## Méthodologie

Pour cette SAÉ, l'objectif est de procéder suivant la méthodologie décrite ci-dessous : 

1. Création de requêtes SQL sur la BD initiale ;
2. Réflexion sur le format des données à obtenir et l’algorithme à réaliser ;
3. Écriture du script Python permettant le passage de SQLite à NoSQL ;
4. S’assurer que la migration s’est bien passée.

## Rendu final

Pour le rendu, il est attendu un rapport ainsi que le code ayant servi à la migration de la base de données.

### :blue_book: Rapport

Le rapport à pour objectif de présenter la migration : contexte, difficultés recontrées, méthodologie, architecture cible, etc. Tout ce qui vous semble pertinent pour discuter de la migration d'une base de données relationnelle vers une base de données NoSQL.

Le rapport doit faire 5 pages maximum (format PDF). Vous pouvez ajouter des images si vous le souhaitez.

Le rapport doit être déposé sur Moodle dans l'onglet **SAÉ - Rapport**.

### :computer: Code

Pour ce qui est du code, vous devez rendre le code (commenté, propre et clair) des séances 1 et 3. Ces codes sont ceux qui vous ont permis de requêter les données `ClassicModel` ainsi que ceux ayant permis la migration de SQLite à MongoDB.

Il est préférable de rendre un notebook Python (les fichiers Python seront également acceptées).

Le code doit être mis sur un repo GitHub dont vous mettrez le lien sur Moodle **SAÉ - Code**.