---
title: Machine virtuelle pré-configurée
weight: 2
---


Il est possible d'installer une VM pré-configurée contenant Cuda, tensorflow, et la plupart des librairies utiles pour le Deep learning.


https://console.cloud.google.com/ai/platform/notebooks/list/instances


Select 1 gpu tesla


Cocher la case "Install NVIDIA GPU driver automatically for me"


Pricing de la VM dans ce cas, ce qui coûte c'est la VM quand elle tourne, et les deux disks de 100Go. 
Du coup pour stopper sans perdre les données vous pouvez faire un snapshot des disks https://console.cloud.google.com/compute/disks et éteindre la VM. Pour reprendre il faudra cliquer sur le snapshot https://console.cloud.google.com/compute/snapshots pour recréer un disk à partir de lui. Ensuite depuis l'instance faudra désigner les deux disks
(Mais sinon vous pouvez tout supprimer, et réimporter quand nécessaire)
