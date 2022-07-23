---
title: "Créer un environnement virtuel avec Venv python"
subtitle: ""
author: Eddine Omar
tags: 
date: 2022-06-01T18:00:00.00Z
draft: false
---
# Introduction
Les environnements virtuels embarquent toutes les dépendances d'un projet Python mais dans un scope plus petit que le scope "système".

Voici pourquoi utiliser un environnement virtuel :
 * Ne pas polluer sa machine
 * Éviter les conflits de dépendances
 * Réduire les problèmes de reproductibilité
 * Contourner les problèmes de privilèges d'installation

Voyons maintenant comment cela s'utilise concrètement.

# Préliminaire : installer les outils
Assurons nous d'avoir les dépendances nécessaire au bon fonctionnement de Python et venv
```bash
sudo apt-get install build-essential libssl-dev libffi-dev python-dev python3-venv
```

# Création, activation et désactivation d'un environnement virtuel
a. Créer un environnement virtuel dans un dossier appelé "venv"
```
# python3 -m venv [nom du dossier]
python3 -m venv venv
```
Un dossier sera crée et contiendra un environnement Python fonctionnel différent de l'environnement du système.

b. Activer l'environnement virtuel
Une fois l'environnement virtuel installé ou lorsqu'un environnement virtuel existe, il convient de l'activer avant de l'utiliser.
Nous allons utiliser la commande suivante :
```
source venv/bin/activate
```

c. Désactiver l'environnement virtuel
Pour désactiver l'environnement virtuel, il suffit de taper la commande `deactivate`
```
source venv/bin/activate
```

# Utilisation
Utilisez le terminal et placez vous dans projet contenant un environnement virtuel puis activez le.
Il est ensuite possible d'effectuer les opérations suivantes :
 - Installer un package dans l'environnemnt virtuel avec la commande `pip install [nom du package]`
 - Installer un fichier de dépendances avec la commande : `pip3 install -r requirements.txt` (si le nom du fichier de dépendances est *requirements.txt*)
 

Maintenant vous êtes en mesure de tester un projet python en local ou de travaillera avec les environnements virtuels avec Python.

# Pour aller plus loin
 * [Virtual Environments and Packages](https://docs.python.org/3/tutorial/venv.html)
 * [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/)
