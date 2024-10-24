# TP3

Pour continuer le TP à la maison, il faudra ajouter votre IP sur le Cluster MongoDB sur Atlas. Pour cela, suivez les étapes suivantes :
1. Aller dans l'onglet "Network Access" de votre Cluster.
2. Cliquer sur "Add Current IP Address".

![Ajout IP](img/ajout-ip.png?raw=true "Ajout IP")

## Commandes git

Pour continuer le TP vous devez cloner votre repository sur votre machine. Pour cela, vous pouvez utiliser la commande suivante :

```bash
git clone URL
```
où `URL` est l'adresse de votre repository (bouton vert `Code` sur GitHub).

Pour ajouter les questions à votre dépôt, vous pouvez utiliser les commandes suivantes :

```bash
git status # permet de vérifier que le fichier est modifié
git add questions.ipynb
git commit -m "Ajout des questions"
git push
```

## Éteindre le cluster

Une fois que vous avez terminé le TP, n'oubliez pas d'éteindre votre cluster.

![Terminate cluster](img/terminate-cluster.png?raw=true "Terminate cluster")