---
title: Création de la VM 
weigth: 0
---
Dans cette partie, nous allons installé une machine google cloud 

## Créer l'instance du serveur Google Cloud

## Création de la VM

<img src="../../instance.png" width="900"/>




* Compute engine => instance VM => Créer
* Région : Europe-west1 (Belgique)
* Zone : europe-west1-b
* Config de machine => Série : N1
* Type de machine : n1-standard-8 (30go)


Dans la liste déroulange "Plate-forme du processeur et GPU" 

* Ajouter un GPU : NVIDIA Tesla K80

* Image ubuntu 20.04 avec un disque dur de 200Go

* Cocher Autoriser le trafic HTTP et HTTPS

{{< hint info >}}
Reportez-vous à [Augmenter les quotas](../../troubleshooting#problème-de-quotas) si vous rencontrez le message d'erreur
"... does not have enough resources available to fulfill the request. Try a different zone, or try again later. "
{{< /hint >}}


