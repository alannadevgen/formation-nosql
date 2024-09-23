# SAÉ NoSQL - Séance 2

La première séance a permis de se familiariser avec la base de données *ClassicModel*. L'objectif de cette séance est de réfléchir à la migration de cette base de données vers un modèle NoSQL.

1. Création de requêtes SQL sur la BD initiale ;
2. Réflexion sur le format des données à obtenir et l’algorithme à réaliser ;
3. Écriture du script Python permettant le passage de SQLite à NoSQL ;
4. Création des requêtes initiales au nouveau format NoSQL pour s’assurer que la migration s’est bien passée.

La première séance nous a permis de faire les requêtes SQL, maintenant nous allons réaliser l'étape 2.

## Réflexion sur la migration

À partir du schéma de la base de données *ClassicModel* ci-dessous, vous devez réfléchir à la ré-organisation des données dans un modèle NoSQL.

![ClassicModel ER](https://github.com/alannadevgen/resources-nosql/blob/main/SAE/img/ClassicModel-ER.png)

L'objectif de la séance est d'accomplir les 3 tâches suivantes :

1. Établir le type de base de données NoSQL à utiliser :  clé-valeur (Redis), colonne (Apache Cassandra), document (MongoDB), graphe (Neo4j) ;
2. Établir le schéma cible des données dans la base de données NoSQL choisie ;
3. Établir le pseudo-algorithme permettant de passer du modèle relationnel au modèle NosSQL.