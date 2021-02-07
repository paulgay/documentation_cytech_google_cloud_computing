---
title: Configuration manuelle de la machine virtuelle 
weight: 0
---


   

### Troubleshoot : Aucune GPU listée :


* `pip3 show tensorflow-gpu` 
Vérifier que tensorflow-gpu==2.2.0 est installé sur l'environnement conda où vous lancez le jupyter.
Cette commande doit retourner la version 2.2 (voir au dessus, pour correspondre au cuda10.2 c'est nécessaire de pas mettre la dernière version dispo)


* `pip3 show tensorflow`
Cette commande ne devrait rien retourner, dans ce cas c'est OK

* Si lorsque vous listez les devices (avec la cellule d'au dessus) vous voyez dans la console : Could not load dynamic library 'libcudart.so.10.2' alors il faut hacker le code tensorflow pour qu'il la trouve (ou réinstaller depuis les sources, c'est ce qu'ils disent sur le tuto mais c'est embêtant)
    * `sudo ln -s /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudart.so.10.2 /usr/lib/x86_64-linux-gnu/libcudart.so.10.2`

* S'il demande une autre version de la librairie libcudart alors c'est qu'il faut que vous changiez la version de tensorflow-gpu pour qu'il change ses prérequis

* Si toujours pas bon, ajoutez ça à la fin du bashrc :
    * `export PATH=/usr/local/cuda-10.2/bin${PATH:+:${PATH}}`
    * `export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`

Ca fonctionnera quand la cellule vous printera une ligne pour le CPU et une ou plusieurs lignes pour la GPU



## TroubleShooting


### Augmenter les quotas 


Passez la limite de "Compute Engine API GPUs (all regions)" à 1:

* Dans la barre de recherche : "Recherchez des produits et des ressoures", tapez `IAM et admin`
* Dans le menu de gauche, allez dans "quotas"
* Cliquez le champ Filter table -> limit name -> faites déroulez la liste jusqu'à trouver GPU all regions.
* Sélectionnez-le, un bandeau doit apparaître à droite de l'écran. Cliquez "global" éditez les quotas  
* Faire une demande pour le passer à 1. (parfois 15 min d'attente avant confirmation par mail)
