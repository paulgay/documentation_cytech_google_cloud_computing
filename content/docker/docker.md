---
title: Running docker on tensorflow 
weigth: 0
---

Étant donné l'usage actuel universel de docker, c'est probablement une bonne idée de prendre du temps pour effectuer cette installation.

{{< hint info >}}
Vous devez avoir au préablable [créé votre VM](../manual_configuration/vm_creation). 
{{< /hint >}}

## A few lines to explain how docker is working 
Installez [docker](https://docs.docker.com/engine/install/ubuntu/) sur votre VM



## Installation de l'image

 

### Installation des drivers nvidia: 

Récupérer la dernière version sur le site de [nvidia](https://www.nvidia.com/en-us/drivers/unix/)

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

Des fichiers docker sont disponibles sur le github de tensorflow: 
```
sudo apt update
sudo apt install git
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow/tensorflow/tools/dockerfiles/
sudo docker build -f ./dockerfiles/gpu-jupyter.Dockerfile -t tf .
sudo docker run -it --gpus all  --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tf:latest
``` 
{{< hint info >}}
It is more simple to download directly from the run command, but then, you don't have the 
```
sudo docker run -it --gpus all  --rm -v $(realpath ~/notebooks):/tf/notebooks -p 8888:8888 tf:latest
```
{{< /hint >}}
