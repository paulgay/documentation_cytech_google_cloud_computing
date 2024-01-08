Cette documentation a pour but de faciliter votre configuration de [GCP](https://console.cloud.google.com/). 

> Vous avez reçu 50 dollars et vous payez à l'heure : pensez à éteindre votre instance quand vous ne l'utilisez pas ! 

Vous avez différentes possibilités pour utiliser tensorflow sur votre machine virtuelle : 

* **Configuration manuelle:** Installation manuelle de toutes les librairies (drivers nvidia, librairies cuda, environnement anaconda, etc)
* **Image docker (recommandé):** Téléchargement d'une image docker contenant tensorflow et qui ne nécessite que les drivers nvidia pour fonctionner. Cependant vous devrez maîtriser l'outil docker si vous souhaitez modifier cette image et ajouter de nouveaux modules. Étant donné l'universalité actuelle de docker, c'est certainement une bonne idée de saisir une occasion pour maîtriser cet outil
* **Machine virtuelle pré-configuré** : Cette option est la plus chère, et vous devez prendre garde à supprimer votre VM à chaque utilisation et à sauvegarder manuellement les données que vous souhaitez conserver.
