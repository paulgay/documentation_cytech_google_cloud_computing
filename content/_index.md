Oyez étudiants de cy-tech, cette documentation a pour but de faciliter votre configuration de [GCP](https://console.cloud.google.com/). 

> Mais n'oubliez jamais: vous avez reçu 50 dollars et vous payez à l'heure : pensez à éteindre votre instance quand vous ne l'utilisez pas ! 

Vous avez différentes possibilités pour utiliser tensorflow sur votre machine virtuelle : 

* **[Configuration manuelle](../../vm_creation/vm_creation) (recommandée):** Installation manuelle de toutes les librairies (drivers nvidia, librairies cuda, environnement anaconda, etc). Heureusement, cette année 2024, il existe une VM sans surcoût où la plupart des dépendances liées à Cuda sont installées.
* **Image docker:** Téléchargement d'une image docker contenant tensorflow et qui ne nécessite que les drivers nvidia pour fonctionner. Cependant vous devrez maîtriser l'outil docker si vous souhaitez modifier cette image et ajouter de nouveaux modules. Étant donné l'universalité actuelle de docker, c'est certainement une bonne idée de saisir une occasion pour maîtriser cet outil
* **Machine virtuelle pré-configuré (non testé depuis 2023)** : Cette option est la plus chère, et vous devez prendre garde à supprimer votre VM à chaque utilisation et à sauvegarder manuellement les données que vous souhaitez conserver.
