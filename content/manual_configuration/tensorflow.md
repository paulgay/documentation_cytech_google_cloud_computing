---
title: Installation de tensorflow
weight: 1
---

Supposons que [votre VM est créée avec les driver nvidia](../../vm_creation/vm_creation/)

Si vous avez utilisez l'image (recommandé) vous pouvez directement [installer tensorflow](../../manual_configuration/tensorflow/#installation-tensorflow)

## installation de Cuda (doc de 2021 non révisée)

Commençons par la librairie Cuda qui permettra à Tensorflow d'utiliser le GPU. 

> the following sections are inspired from the [official documentation](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html)

Clikez sur le bouton ssh afin d'ouvrir un terminal sur votre machine virtuelle. 

Sélectionner un mode de téléchargement sur le site de [cuda](https://developer.nvidia.com/cuda-11.0-download-archive). 
A l'heure actuelle (février 2021), tensorflow a été compilé avec la version 11.0 de cuda. Nous choisirons donc cette version.

<center>
<img src="../../cuda.png" alt="drawing" width="900"/>
</center>


Ensuite, exécutez les commandes suivantes: 

```
sudo apt udpate
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/11.0.2/local_installers/cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-0-local_11.0.2-450.51.05-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```

Ajoutez les lignes suivantes dans le fichier `~/.bashrc`
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
export PATH=$PATH:/usr/local/cuda/bin/
```

Puis exécutez la commande suivante: 
```Shell
source .bashrc
```

Ensuite, installez [cudnn](https://developer.nvidia.com/rdp/cudnn-archive). Il vous sera demandé de créer un compte. Vous pourrez ensuite télécharger les fichiers `.deb` et utiliser la commande `dpkg` pour les installer.
```
sudo dpkg -i libcudnn8_8.0.5.39-1+cuda11.0_amd64.deb
sudo dpkg -i libcudnn8-dev_8.0.5.39-1+cuda11.0_amd64.deb
```

## Environnement Anaconda 

* Récupérez l'installeur d'Anaconda sur la [page des téléchargements](https://www.anaconda.com/products/individual). 
Choisissez celui pour linux en 64 bits et téléchargez-le, par exemple avec:
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh
``` 

* `bash Anaconda3-5.1.0-Linux-x86_64.sh`

utilisez les défauts et accepter l'initialisation
```
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
```
* Redémarrez votre shell ou rechargez votre fichier avec `source ~/.bashrc`

## Installation Tensorflow

* Installez tensorflow depuis votre environnement conda
```bash
(base) pandregay@instance-1:~$ pip install tensorflow[and-cuda] 
```
* Testez que tensorflow a accès à votre gpu: 
```python
import tensorflow as tf
print(tf.config.list_physical_devices('GPU'))
```

    [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]


