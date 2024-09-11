
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

