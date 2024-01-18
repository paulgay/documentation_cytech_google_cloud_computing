---
title: Troubleshooting 
weight: 10
---

## Problème de quotas 


Passez la limite de "Compute Engine API GPUs (all regions)" à 1:


* IAM et admin => quotas
* Cliquez le champ Filter table -> limit name -> faites déroulez la liste jusqu'à trouver GPU all regions.
* Sélectionnez-le, puis, cliquez sur le bouton "modifier les quotas".
* Dans le champ, inscrivez le chiffre 1. Écrivez dans le deuxième champ un message simple "I need a GPU". (parfois 15 min d'attente avant confirmation)


