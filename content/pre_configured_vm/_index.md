---
title: Machine virtuelle pré-configurée
weight: 3
---


Il est possible d'installer une VM pré-configurée contenant Cuda, tensorflow, et la plupart des librairies utiles pour le Deep learning.


https://console.cloud.google.com/ai/platform/notebooks/list/instances
avec les options: 

* Select 1 gpu tesla
* "Install NVIDIA GPU driver automatically for me"

Cependant, cette VM vous coûte de l'argent même quand elle est éteinte. Vous pouvez choisir de la supprimer après chaque utilisation, mais ceci vous oblige à regénérer tout votre environnement à chaque fois ainsi que les données que vous souhaitez y stocker. 

Pour conserver les données, vous pouvez faire [une sauvegarde des disques](https://console.cloud.google.com/compute/disks) et éteindre ensuite la VM. Pour reprendre il faudra cliquer sur le [snapshot](https://console.cloud.google.com/compute/snapshots) pour recréer un disque à partir de ce dernier. 
