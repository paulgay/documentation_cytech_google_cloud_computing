---
title: Création de la VM 
weigth: 0
---
Dans cette partie, nous allons installé une machine google cloud 

## Créer l'instance du serveur Google Cloud

## Création de la VM

<img src="../../instance.png" width="900"/>




* Aller à _Compute engine => instance VM => Créer une instance_



* then select region _Région : northamerica-northeast1-c_  Notez que les GPUs ne sont pas toujours disponibles partout. Malheureusement, GCP ne propose pas de zone automatiquement.

Dans la rubrique *Configuration de la machine*

sélectionner _GPU_ avec la configuration suivante 

* Type de GPU : NVIDIA T4 

* Nombre de GPU : 1

* Type de machine : PRÉDÉFINI avec 8vCPU, 30 Go


Dans la sélection de l'OS, cliquer sur _changer d'image_ et prendre 
 * Deep Learning VM with CUDA 11.8 M114


laisser les autres paramètres par défaut et cliquer sur créer




{{< hint info >}}
Reportez-vous à [Augmenter les quotas](../../troubleshooting#problème-de-quotas) si vous rencontrez le message d'erreur
"... does not have enough resources available to fulfill the request. Try a different zone, or try again later. "
{{< /hint >}}


## Installation des drivers nvidia (Debian):

> Il est plus simple d'éviter cette étape avec une machine pré-configuré en sélectionnant l'image _Deep Learning VM with CUDA 11.8 M114_


Que ce soit docker ou une installation manuelle, il faut installer les drivers nvidia. 

Notre image est une debian, 


Gardez les options par défaut lors de l'installation
choose english

Restart without asking 

Keep the local version currently installed

> N'oubliez pas de redémarrer la VM!
sudo shutdown -r


```
sudo apt-get install ubuntu-drivers-common
ubuntu-drivers devices
```
    == /sys/devices/pci0000:00/0000:00:04.0 ==
    modalias : pci:v000010DEd0000102Dsv000010DEsd0000106Cbc03sc02i00
    vendor   : NVIDIA Corporation
    model    : GK210GL [Tesla K80]
    driver   : nvidia-driver-450-server - distro non-free
    driver   : nvidia-driver-460 - distro non-free recommended
    driver   : nvidia-driver-390 - distro non-free
    driver   : nvidia-driver-418-server - distro non-free
    driver   : nvidia-driver-450 - distro non-free
    driver   : xserver-xorg-video-nouveau - distro free builtin

Nous installons la version recommandée (ici la 460):
```
sudo apt install nvidia-driver-460

