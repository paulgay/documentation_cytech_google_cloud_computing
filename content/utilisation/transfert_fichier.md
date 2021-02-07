---
title: Transfert de fichiers
weight: 1
---

## Uploadez des fichiers sur sa machine locale 


### Par ssh


* Ajout de la clé publique SUR VOTRE MACHINE PERSONNELLE : 
    * copier l'intégralité du fichier `~/.ssh/id_rsa.pub` (le créer avec la commande `ssh-keygen` s'il n'existe pas)
    * le coller SUR LA MACHINE GCP dans le fichier ~/.ssh/authori 


* Ensuite, pour copier MON_FICHIER de la machine locale vers la VM `scp /chemin/vers/MON_FICHIER  login@address_ip_externe:/chemin/sur/la/VM`

## buckets

