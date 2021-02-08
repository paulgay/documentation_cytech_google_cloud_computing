---
title: Troubleshooting 
weight: 10
---

## Problème de quotas 


Passez la limite de "Compute Engine API GPUs (all regions)" à 1:


* IAM et admin => quotas
* Cliquez le champ Filter table -> limit name -> faites déroulez la liste jusqu'à trouver GPU all regions.
* Sélectionnez-le, un bandeau doit apparaître à droite de l'écran. Cliquez "global" éditez les quotas  
* faire une demande pour le passer à 1. (parfois 15 min d'attente avant confirmation)

