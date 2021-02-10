---
title: Connection à la VM et transfert de fichiers 
weight: 1
---
## Connection en ssh par le site google cloud

Le tableau de bord vous donne l'adresse ip actuelle de votre VM. Vous pouvez cliquez sur le bouton ssh afin d'y ouvrir un terminal. 
<img src="https://paulgay.github.io/documentation_cytech_google_cloud_computing/ssh.png" width="900"/>


La section suivante détaille comment lancer vos propres commandes depuis votre machine locale. C'est parfois nécessaire, par exemple pour créer des tunnels afin de copier des fichiers ou d'accéder au serveur jupyter. 

## Connection en ssh depuis votre machine locale

Il faut ajouter votre clé publique qui est sur votre machine locale dans le fichier `authorized_keys` de votre VM.

Il faut d'abord configurer votre serveur pour qu'il accepte des connections venant de votre ordinateur. Pour cela, copiez votre clé publique sur le serveur

* Dans "Compute Engine -> Instance de VM -> Métadonnées"
* Séléctionnez l'onglet "Clés SSH" puis le bouton "Modifier"
<center>
<img src="https://paulgay.github.io/documentation_cytech_google_cloud_computing/add_public_key.png" alt="drawing" width="900"/>
</center>

Copiez l'intégralité du fichier présent sur votre machine locale avec pour chemin `~/.ssh/id_rsa.pub`
Si ce fichier n'existe pas, vous pouvez le générer avec la commande `ssh-keygen`

* Vérifiez que votre clé publique est bien présente sur la VM dans le fichier `~/.ssh/authorized_keys`

> Note: il n'est pas conseillé de copier directement votre clé publique dans le fichier `authorized_keys` car google utilise des processus interne qui ré-écrivent ce fichier à partir de la configuration que vous avez indiqué sur leur site.

## Uploadez des fichiers sur sa machine locale 


### Par ssh

Pour copier MON_FICHIER de la machine locale vers la VM 
```
scp /chemin/vers/MON_FICHIER  login@address_ip_externe:/chemin/sur/la/VM
```

## buckets

