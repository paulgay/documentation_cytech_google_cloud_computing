---
title: Installation de Tensorflow avec docker 
weigth: 0
---

Une image docker fournit un environnement pré-installé et fonctionnel. Le principe général se situe entre la machine virtuelle et l'environnement virtuel. 

Étant donné l'usage actuel universel de docker, c'est probablement une bonne idée de prendre du temps pour effectuer cette installation.

{{< hint info >}}
Vous devez avoir au préablable [créé votre VM](../manual_configuration/vm_creation). 
{{< /hint >}}


Depuis votre VM [connectez-vous en ssh](../../utilisation/transfert_fichier) et installez [docker](https://docs.docker.com/engine/install/ubuntu/) sur votre VM

L'installation consiste à ajouter les drivers nvidia, puis à télécharger un conteneur docker qui contiendra la librairie tensorflow avec les dépendances cuda.  

### Installation des drivers nvidia: 


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

### Installation du container nvidia
Créer un fichier `nvidia-container-runtime-script.sh` avec le contenu suivant: 


```
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update
```
Puis installez le conteneur nvidia
```
sudo apt-get install nvidia-container-runtime
sudo systemctl restart docker
```

Re-démarrez votre machine. 

### Installation de l'image docker

Des fichiers Dockerfile sont disponibles sur le github de tensorflow: 
```
sudo apt update
sudo apt install git
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow/tensorflow/tools/dockerfiles/
sudo docker build -f ./dockerfiles/gpu-jupyter.Dockerfile -t tf .
```

> ces commandes doivent être exécutées depuis le repertoire `tensorflow/tools/dockerfiles` car elles supposent que certains fichiers (comme le fichier bashrc) sont disponibles dans le répertoire courant.

La dernière ligne est la commande qui construit votre image sous le nom de `tf`. Pour lancer le notebook
```
sudo docker run -it --gpus all  --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tf:latest
``` 
À présent, votre jupyter est lancé sur le port 8888 et l'adresse `localhost` de la VM. 
Le répertoire qui contient vos notebook est indiqué dans la commande. Dans cet exemple, il s'agit de `~/notebooks`. Notez que l'environnement docker n'a pas accès aux autres répertoires de votre VM.

Consultez [cette section](../../manual_configuration/jupyter/) pour accéder au jupyter de votre VM.

{{< hint info >}}
Vous pouvez aussi télécharger directement à partir de la commande `run`. L'avantage de passer par le fichier `.Dockerfile` est que vous pouvez l'adapter pour y ajouter d'autres librairies dont vous pourriez avoir besoin.
```
sudo docker run -it --gpus all  --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tf:latest
```
{{< /hint >}}



### Ajout de modules supplémentaires

L'image docker et les libraires qu'elle contient sont spécifiées dans les fichiers *.Dockerfile.

Il est indiqué dans le README du github de tensorflow qu'il n'est pas conseillé de modifier directement ces fichiers Dockerfile. 
Il est proposé à la place de modifier un ficher de configuration et d'utiliser un script python pour générer les fichiers Dockerfile.

