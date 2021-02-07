---
title: Jupyter notebook
weight: 2
---

## Jupyter notebook : option1 : tunnel ssh

Il existe plusieurs manières, nous décrivons ici l'utilisation d'un tunnel ssh:

### Ajout de la clé publique. 

Il faut d'abord configurer votre serveur pour qu'il accepte des connections venant de votre ordinateur. Pour cela, copiez votre clé publique sur le serveur


* Dans "Compute Engine -> Instance de VM -> Métadonnées"
* Séléctionnez l'onglet "Clés SSH" puis le bouton "Modifier"
<center>
<img src="/add_public_key.png" alt="drawing" width="900"/>
</center>

Copiez l'intégralité du fichier `~/.ssh/id_rsa.pub`
Si le fichier n'existe pas, vous pouvez le générer avec la commande `ssh-keygen`


À présent, ouvrez un tunnel ssh connectant votre machine à votre VM.
```
ssh -X -L 8099:localhost:8099 pandregay@adresse_ip_externe
```

Depuis la VM, lancez votre jupyter:

```
jupyter-notebook --no-browser --port=8099
```
    ...
    To access the notebook, open this file in a browser:
        file:///home/pandregay/.local/share/jupyter/runtime/nbserver-18405-open.html
    Or copy and paste one of these URLs:
        http://localhost:8099/?token=2703d92e3badf239641b349d2f5c4e9828cf3968f3c0926c

Dans ce cas, vous accédez à votre notebook en copiant l'adresse 
```
http://localhost:8099/?token=2703d92e3badf239641b349d2f5c4e9828cf3968f3c0926c
```
dans votre navigateur.



L'url que vous entrez dans le navigateur doit avoir la forme : `http://adresse_ip_externe:8889/?token=votre_token`


## Jupyter noteboook option2 : configuration des pare-feu et addresse IP static

## Configuration des firewalls pour Jupyter

Sur le site de Google Cloud platform, allez dans [Réseaux VPC, ](https://console.cloud.google.com/networking/networks/)


### Créer une IP externe


[addresse IP Externe](https://console.cloud.google.com/networking/addresses/) :


* Passez de éphémère à static
* Mettre un nom sur l'addresse IP


### Ajouter une règle firewall


Dans [pare-feu](https://console.cloud.google.com/networking/firewalls) 


* Vérifiez default-allow-ssh => tcp:22
* Dans cible choissisez "toutes les instances du réseau"
* Dans plage d'adresse IP : 0.0.0.0/0
* Protocole et port spécifié: TCP 22: 8889


## installation de jupyter sur la VM

* `jupyter notebook --ip=0.0.0.0 --port=8889 --no-browser &`


Accéder au Jupyter :

* copier l'adresse à partir de "?token=....."
* Ajouter devant le "?" l'adresse externe de votre VM (dans instance VM) et :8889.n


L'url que vous entrez dans le navigateur doit avoir la forme : `http://adresse_ip_externe:8889/?token=votre_token`


