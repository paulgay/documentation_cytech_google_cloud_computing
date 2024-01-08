---
title: Jupyter notebook
weight: 2
---

Vous pouvez au choix configurez l'adresse IP et les parefeux de votre VM ou utliser un tunnel ssh.

## Jupyter notebook : option1 : tunnel ssh

> Pré-requis : [ajouter sa clé publique](../../utilisation/transfert_fichier/#connection-en-ssh-depuis-votre-machine-locale) à la VM pour pourvoir s'y connecter en ssh depuis votre machine locale. 

Ouvrez un tunnel ssh connectant votre machine au localhost de votre VM.
```
ssh -X -L 8888:localhost:8888 pandregay@adresse_ip_externe
```
Notez que le numéro du port doit correspondre à celui sur lequel votre Jupyter tourne.

Depuis la VM, lancez votre jupyter (si vous ne l'avez pas déjà fait par le biais de votre image docker):

```
jupyter-notebook --no-browser --port=8888
```
    ...
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=2703d92e3badf239641b349d2f5c4e9828cf3968f3c0926c

Copiez l'adresse affichée par la commande dans votre navigateur en incluant le token:
```
http://localhost:8888/?token=2703d92e3badf239641b349d2f5c4e9828cf3968f3c0926c
```
si vous avez une page vide "a jupyter server is running", ajoutez `/tree` à l'url du navigateur pour avoir
```
http://127.0.0.1:8888/tree
```


## Jupyter noteboook option2 : configuration des pare-feu et addresse IP statique (non testé en 2023)

## Configuration des firewalls pour Jupyter

Sur le site de Google Cloud platform, allez dans [Réseaux VPC](https://console.cloud.google.com/networking/networks/)


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

L'url que vous entrez dans le navigateur doit avoir la forme : `http://adresse_ip_externe:8889/?token=votre_token`

* `votre_token`, correspond à la chaine de caractère dans l'adresse à partir de "?token=....."
