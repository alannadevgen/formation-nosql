
# Installation et configuration MongoDB

## Configuration de la base de données

### Création du compte Atlas

Nous allons créer un [compte Atlas](https://account.mongodb.com/account/register?signedOut=true) afin de pouvoir héberger une base de données MongoDB.

### Création d'un projet Atlas

Une fois que vous avez créé votre compte vous allez pouvoir créer un projet, nommé `but-sd` ici. Ensuite, une page demandera d'ajouter des membres, il n'y a rien à faire. Confirmez simplement la création du projet en cliquant sur **Create project**.

![Creation project](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/creation-project.png)

### Création d'un utilisateur Atlas

Une fois ceci fait on aura besoin de créer un utilisateur, afin de pouvoir requêter la base de données. Pour cela, dans le menu à gauche, cliquez sur **Database access**.

![Create user](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/create-user.png)

Une fois sur la page des **Database access** cliquez sur **Add new database user** afin d'ajouter un utilisateur de la base de données. Cela ouvrira un nouvel onglet comme ci-dessous. Il faudra ainsi définir son nom, son mot de passe et son rôle. Dans notre cas, nous appelerons notre utilisateur `user_mongo` et nous générerons le mot de passe aléatoirement en cliquant sur **Autogenerate Secure Password**. Enfin, nous lui assignerons le rôle d'administrateur Atlas.

![Creation user](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/creation-user.png)

> [!CAUTION]
> Pensez à bien enregistrer le mot de passe dans un endroit sécurisé de votre ordinateur et ne pas le mettre sur un repo public GitHub.

Une fois ceci fait vous aurez la vue suivante : 

![User created](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/user-created.png)

### Création d'un cluster Atlas

Maintenant nous pouvons créer un cluster qui hébergera notre base de données.

![Create cluster](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/create-cluster.png)

Nous prenons l'instance M0 qui est gratuite et donnons un nom à cette dernière, ici `cluster-but-sd`. Il n'y a pas besoin de changer les autres paramètres.

![Creation cluster](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/creation-cluster.png)

### Connexion au cluster Atlas

Enfin, la dernière étape consiste à choisir le connecteur à la base de données. Dans notre cas, nous utiliserons l'API Python donc nous sélectionnons **Drivers**.

![Connection method](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/connection-method.png)

Sur la page suivante nous pouvons choisir le type de Driver, Python dans notre cas.

![MongoDB driver](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/mongodb-driver.png)

> [!NOTE]  
> Pensez à copier la *connection string*, cela nous servira ensuite à nous connecter en Python à la base de données que nous venons de créer.

## Installation de MongoDB Compass

Pour visualiser les données de notre base de données, nous allons installer [MongoDB Compass](https://downloads.mongodb.com/compass/mongodb-compass-1.44.7-win32-x64.exe). Pour cela, cliquez sur le lien et suivez les instructions d'installation.

## Connexion à MongoDB Compass

Maintenant nous allons pouvoir utiliser le cluster créé sur Atlas. Commençons par se connecter à notre instance.

![Compass connection](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/compass-connection.png)

La connexion va se faire via la *connection string* qui peut être trouvée dans la configuration du cluster Atlas. 

> [!CAUTION]
> N'oubliez pas de remplacer le mot de passe sur l'image ci-dessous par celui que vous avez enregistré plus haut.

![Compass add connection](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/compass-add-connection.png)

Une fois ceci fait, nous allons créer une base de données appelée `tp` qui contiendra une collection nommée `restaurants`.

![Create database](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/create-database.png)

## Import des données

Ensuite, il suffit d'importer le fichier JSON qui se situe [ici](https://github.com/alannadevgen/formation-nosql/blob/main/TP/TP1/restaurants.json).

![Import data](https://github.com/alannadevgen/resources-nosql/blob/main/TP/TP1/img/import-data.png)

## Interrogation des données MongoDB en Python

Pour requêter les données dans notre base de données nous allons utiliser le package [`pymongo`](https://docs.mongodb.com/drivers/pymongo/), que l'on peut installer via :

```bash
pip install pymongo
```

Et voilà, vous êtes prêts à requêter les données ! :tada: 

Avant de commencer le [TP](https://github.com/alannadevgen/formation-nosql/blob/main/TP/TP1/tp1.md), lisez les notes sur [le modèle MongoDB](https://github.com/alannadevgen/formation-nosql/blob/main/TP/model-mongodb.md) et [comment requêter les données MongoDB](https://github.com/alannadevgen/formation-nosql/blob/main/TP/query-mongo.md).
