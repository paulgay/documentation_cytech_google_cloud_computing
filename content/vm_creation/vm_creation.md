---
title: Création de la VM 
weigth: 0
---
Dans cette partie, nous allons installer une machine google cloud 

## Créer l'instance du serveur Google Cloud

## Création de la VM

<img src="../../instance.png" width="900"/>



* Aller à _Compute engine => instance VM => Créer une instance_



* Sélectionner la région _Région : northamerica-northeast1-c_  Notez que les GPUs ne sont pas toujours disponibles partout. Malheureusement, GCP ne propose pas de zone valide automatiquement, essayez-en jusqu'à ce que ça marche.

Dans la rubrique *Configuration de la machine*

sélectionner _GPU_ avec la configuration suivante 

* Type de GPU : NVIDIA T4 

* Nombre de GPU : 1

* Type de machine : PRÉDÉFINI avec 8vCPU, 30 Go


Dans la sélection de l'OS, cliquer sur _changer d'image_ et prendre  (une image avec les driver nvidia installés par défaut)
 * Deep Learning VM with CUDA 11.8 M114



laisser les autres paramètres par défaut et cliquer sur créer


{{< hint info >}}
Reportez-vous à [Augmenter les quotas](../../troubleshooting#problème-de-quotas) si vous rencontrez le message d'erreur
"... does not have enough resources available to fulfill the request. Try a different zone, or try again later. "
{{< /hint >}}

## Test de la VM

Vous avez donc créer votre VM, 

<img src="../../main_screen.png" width="900"/>

Le bouton avec les 3 points à droite permet de la démarrer, de l'arrêter et de la re-démarrer. 

Le bouton connecter vous permet d'y accéder par ssh depuis votre navigateur. Une fois le terminal ouvert, vous pouvez noter votre login dans le prompt. Apparemment, il correspond à la première partie du compte gmail que vous utiliser pour vous connecter.

## Installation des drivers nvidia


> Il est plus simple d'éviter cette étape avec une machine pré-configuré en sélectionnant l'image _Deep Learning VM with CUDA 11.8 M114_

Que ce soit docker ou une installation manuelle, il faut installer les drivers nvidia. 


> Une fois l'installation effectuée, n'oubliez pas de redémarrer la VM!
sudo shutdown -r

Ensuite, vous pouvez tester si le gpu est détecté par le driver avec la commande

```
nvidia-smi
```

### Installation des drivers nvidia (Debian):




Pour Debian, [la documentation est ici](https://wiki.debian.org/NvidiaGraphicsDrivers)

```
Add "contrib", "non-free" and "non-free-firmware" components to /etc/apt/sources.list, for example:

# Debian Sid
deb http://deb.debian.org/debian/ sid main contrib non-free non-free-firmware
```

Puis lancez les commandes :
```
apt update
apt install nvidia-driver firmware-misc-nonfree
```


Gardez les options par défaut lors de l'installation
choose english

Restart without asking 

Keep the local version currently installed


> N'oubliez pas de redémarrer la VM!
sudo shutdown -r

### Installation des drivers nvidia (Ubuntu):

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
```

> N'oubliez pas de redémarrer la VM!
sudo shutdown -r
