---
title: "Sécuriser facilement son serveur en quelques étapes"
subtitle: "Comment sécuriser son VPS en ligne ?"
author: Eddine Omar
tags: DevOps
date: 2022-07-21T18:00:00.00Z
draft: false
---
# Introduction

Aussi tôt que votre VPS sera instancié en ligne, de nombreux robots malveillants essaieront de pénétrer dans votre machine. C'est ainsi sur internet. Pour éviter les intrusions, nous allons apprendre comment sécuriser son VPS !

Vous n'êtes pas obligé d'appliquer toutes les mesures dans cet articles, mais une règle du pouce est de s'éloigner de la configuration par défaut en matière de sécurité car les bots essaieront de pénétrer votre serveur en essayant des combines qui exploitent les paramètres par défaut de votre machine.

Disclaimer : il est possible que vous perdiez l'accès à votre VPS pendant la manipulation (la configuration du parefeu), entrainez vous sur un VPS sandbox avant de répercuter les apprentissages dans vos VPS de prod par mesure de sécurité ;-)... Où vous paierez les frais de scolarité :-P

NB : j'utilise un VPS sous Ubuntu Server 22.04 LTS

Voici les étapes que nous allons voir ensemble :
1. Appliquer les mises à jour
2. Changer le port SSH
3. S'authentifier avec une clé SSH
4. Supprimer l'authentification par mot de passe
5. Configurer un pare-feu : ufw
6. Installer et configurer fail2ban

# 1. Appliquer les mises à jour
Un moyen simple de garder son VPS sécurisé, notamment contre les failles CVE, est d'appliquer les mises à jour de sécurité.
Sur une machine Ubuntu, on peut appliquer les mises à jour avec la commande :

```
sudo apt update && sudo apt upgrade -y
```

Voilà, effectuez les mises à jour aussi souvent que nécessaire.

# 2. Changer le port SSH
Généralement on accède au VPS au travers d'une connexion SSH avec nom d'utilisateur et mot de passe. Le port par défaut du service SSH est le 22. Changeons ce numéro de port !

a. Ouvrir le fichier `/etc/ssh/sshd_config` à l'aide de vim (ou de n'importe quel éditeur de fichier) avec les droits super utilisateur :

```
sudo vim /etc/ssh/sshd_config
```

b. Identifier la ligne qui permet de configurer le numéro de port SSH : `#Port 22`

c. Décommentez cette ligne et remplacez 22 par une autre valeur, disons 42 : `Port 42`

d. Relancer le service ssh : `sudo service ssh restart`

e. Pour vous connectez en SSH, utiliser le paramètre -p : `ssh user@hostname -p 42`

Voilà !

# 3. S'authentifier avec une clé SSH
Pour s'authentifier avec une clé SSH (avec un algo comme RSA, ECDSA, DSA etc...), il faut procéder en quelques étapes :

a. Créer une clé dans son ordinateur : `ssh-keygen -t ECDSA -b 4096`, mettez un mot de passe fin de protéger les cas où la clé fuite (cela peut arriver). Ne mettez pas de mot de passe dans les cas où vous souhaitez automatiser des process !

b. Copiez la clé dans votre serveur avec ssh-copy-id :
```
ssh-copy-id -i ~/.ssh/maclessh user@hostname -P PORT
```
Cette commande va automatiquement copier la clé dans votre serveur au bon endroit. Vous devriez vous connectez sur votre serveur sans avoir à saisir de mot de passe avec la commande.
```
ssh user@hostname -p PORT
```

# 4. Supprimer l'authentification par mot de passe
Une fois la connexion avec clé SSH configurée et testée avec succès, on peut désactiver la connexion SSH via mot de passe.
a. Ouvrir le fichier `/etc/ssh/sshd_config` à l'aide de vim (ou de n'importe quel éditeur de fichier) avec les droits super utilisateur :

```
sudo vim /etc/ssh/sshd_config
```
b. Modifier la ligne
```
PasswordAuthentication yes
```
en 
```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes
```

On redémarre le service SSH :
```
sudo service ssh restart
```

Connectez vous à votre VPS comme dans la méthode au point 3.

# 5. Configurer un pare-feu : ufw
/!\ Attention : soyez prudent car vous pouvez perdre l'accès à votre serveur, si vous activez le parfeu et vous déconnectez du serveur sans avoir autoriser le service SSH.
## Installation et configuration de ufw
'ufw' pour uncomplicated firewall est un outil qui permet de définir des règles de sécurité liées au réseau (adresses IP, port, adresses MAC notamment).

ufw est généralement installé dans la plupart des distributions basées sur Ubuntu. S'il n'est pas installté, faites avec la commande :
```
sudo apt install ufw -y
```

La structure de commande de ufw est la suivante : 
```
ufw [--dry-run] [options] [rule syntax]
```

Nous allons maintenant configurer les parefeu ufw pour autoriser les services dont nous avons besoin. Nous allons autoriser le port lié au service SSH avec la commande :
```
# activer le parefeu
sudo ufw enable
```

```
# autoriser le port 42
sudo ufw allow 42/tcp
```

on peut aussi utiliser un alias :
```
# autoriser le service ssh si on ne connait pas le port
sudo ufw allow ssh/tcp
```

Si un serveur web (apache2, nginx) écoute sur les ports 80 et 443 nous allons autoriser ces ports comme ceci :
```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# en utilisant les alias ci-dessous
#sudo ufw allow http/tcp
#sudo ufw allow https/tcp
```

## Vérification du status et des règles ajoutées
Pour inspecter les paramètres appliquées à ufw, utilisez la commande status
```bash
user@hostname:~$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW IN    Anywhere                  
443/tcp                    ALLOW IN    Anywhere                  
42/tcp                     ALLOW IN    Anywhere                  
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443/tcp (v6)               ALLOW IN    Anywhere (v6)             
42/tcp (v6)                ALLOW IN    Anywhere (v6)             
```

# 6. Installer et configurer fail2ban
"fail2ban est une application qui analyse les logs de divers services (SSH, Apache, FTP…) en cherchant des correspondances entre des motifs définis dans ses filtres et les entrées des logs. Lorsqu'une correspondance est trouvée une ou plusieurs actions sont exécutées. Typiquement, fail2ban cherche des tentatives répétées de connexions infructueuses dans les fichiers journaux et procède à un bannissement en ajoutant une règle au pare-feu iptables ou nftables pour bannir l'adresse IP de la source." [Source](https://doc.ubuntu-fr.org/fail2ban)

a. Installer fail2ban
```
sudo apt update && sudo apt install fail2ban -y
```

b. Créer une copie du fichier jail.conf
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

c. Créer des règles sous l'élément sshd
Voici un exemple de configuration pour le service SSH sur le port 42 :
```
[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
#mode   = normal
port    = 42
logpath = %(sshd_log)s
backend = %(sshd_backend)s
enabled = true
filter = sshd
max_retry = 3
findtime = 5m
bantime = 30m
```

d. Activer le service SSH
```
sudo service ssh start
```

e. Vérifier le bon fonctionnement de la configuration fail2ban pour le service SSH
```
$ sudo fail2ban-client status sshd
user@hostname:~$ sudo fail2ban-client status sshd
Status for the jail: sshd
|- Filter
|  |- Currently failed:	0
|  |- Total failed:	0
|  `- File list:	/var/log/auth.log
`- Actions
   |- Currently banned:	0
   |- Total banned:	0
   `- Banned IP list:	
```

# En savoir plus
- [https://doc.ubuntu-fr.org/fail2ban](https://doc.ubuntu-fr.org/fail2ban)
- [https://linuxconfig.org/how-to-install-and-use-ufw-firewall-on-linux](https://linuxconfig.org/how-to-install-and-use-ufw-firewall-on-linux)
