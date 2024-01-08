---
title: Connection ssh et transfert de fichiers 
weight: 2
---
## Connection en ssh par le site google cloud

Le tableau de bord vous donne l'adresse ip actuelle de votre VM. Notez que cette adresse changera à chaque démarrage à moins que ne vous ne la configuriez statique.

Vous pouvez cliquez sur le bouton ssh afin d'y ouvrir un terminal. Cela ouvrira un prompt dans un navigateur. Ce prompt vous permet de noter votre login gcp, qui correspond normalement à la première partie de l'adresse mail utilisée pour vous connecter.
<img src="../../main_screen.png" width="900"/>

Enfin, notez également à cette endroit l'adresse IP externe de votre machine.


La section suivante détaille comment lancer vos propres commandes ssh depuis votre machine locale (ou comme il est écrit sur le site de gcp, depuis un outil tiers). C'est parfois nécessaire, par exemple pour créer des tunnels afin de copier des fichiers ou d'accéder au serveur jupyter. 

## Connection en ssh depuis votre machine locale

En théorie, la clé publique qui est sur votre machine locale doit apparaître dans le fichier `~/.ssh/authorized_keys` de votre VM. 

> Note: il n'est pas conseillé de copier directement votre clé publique dans le fichier `authorized_keys` car google utilise des processus internes qui ré-écrivent et écrasent régulièrement ce fichier. 

Une solution est d'ajouter votre clé publique dans les métadonnées de votre VM.

* Dans "Compute Engine -> Instance de VM -> Métadonnées"
* Séléctionnez l'onglet "Clés SSH" puis le bouton "Modifier"
<center>
<img src="../../add_public_key.png" alt="drawing" width="900"/>
</center>

Copiez l'intégralité du fichier présent sur votre machine locale `~/.ssh/id_rsa.pub`

Si ce fichier n'existe pas, vous pouvez le générer avec la commande `ssh-keygen -t rsa`

Formattez ensuite l'affichage de votre clé pour qu'elle ressemble à:
```
ssh-rsa token_long_list_of_characters google-ssh {"userName":"your_gcp_login","expireOn":"2023-02-10T23:16:51+0000"}
```

`your_gcp_login` correspond généralement à la 1ère partie de l'adresse gmail que vous utilisez pour vous connecter à GCP. Vous pouvez vous le vérifiez avec le prompt bash qui apparait quand [vous vous connnectez en ssh depuis la page web](../../vm_creation/vm_creation/#test-de-la-vm)

* Vérifiez ensuite que votre clé publique est bien présente sur la VM dans le fichier `~/.ssh/authorized_keys`

Vous pouvez vous connecter normalement en ssh 
```
ssh your_gcp_login@address_ip_externe
```

## Uploadez des fichiers de sa machine locale vers la VM


### Par ssh

Pour copier MON_FICHIER de la machine locale vers la VM 
```
scp /chemin_local/vers/MON_FICHIER  login@address_ip_externe:/chemin/sur/la/VM
```

### Autoriser les requêtes http sur votre site web

En deux mots, il s'agit de pouvoir récupérer des fichiers situés sur votre machine virtuelle à partir d'une requette http (par exemple, en entrant une url dans votre navigateur).


Pour cela, il est proposé d'utiliser nginx.
```
https://jkjung-avt.github.io/gcp-nginx-flask/
```
