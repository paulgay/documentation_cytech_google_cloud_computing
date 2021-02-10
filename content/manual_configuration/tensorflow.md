---
title: Installation de tensorflow
weight: 1
---

Commençons par la librairie Cuda qui permettra à Tensorflow d'utiliser le GPU. 

## installation de Cuda

Clikez sur le bouton ssh afin d'ouvrir un terminal sur votre machine virtuelle. 

Sélectionner un mode de téléchargement sur le site de [cuda](https://developer.nvidia.com/cuda-11.0-download-archive). 
A l'heure actuelle, tensorflow a été compilé avec la version 11.0 de cuda. Nous choisirons donc cette version.

<center>
<img src="../../cuda.png" alt="drawing" width="900"/>
</center>


Ensuite, exécutez donc les commandes suivantes: 

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
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64export" 
export PATH=$PATH:/usr/local/cuda/bin/" 
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


Pour vérifier que l'installation a fonctionné, nous pouvons tester la commande `nvidia-smi`: 
```
$ nvidia-smi


Wed Feb  3 10:20:31 2021       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 460.32.03    Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla K80           Off  | 00000000:00:04.0 Off |                    0 |
| N/A   71C    P8    35W / 149W |     13MiB / 11441MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A       937      G   /usr/lib/xorg/Xorg                  8MiB |
|    0   N/A  N/A      1081      G   /usr/bin/gnome-shell                3MiB |
+-----------------------------------------------------------------------------+
```

Une information intéressante est la quantité de mémoire occupée `12MiB / 11441MiB`. Cette information est utile lorsque nous entraînons nos modèles et pour vérifier si notre gpu est utilisé ou pas. 

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
* Redémmarez votre shell ou rechargez votre fichier `source ~/.bashrc`

* Installez tensorflow depuis votre environnement conda
```bash
(base) pandregay@instance-1:~$ pip install tensorflow
```
* Testez que tensorflow a accès à votre gpu: 
```python
import tensorflow as tf
physical_devices = tf.config.list_physical_devices('GPU')
```

    [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]


