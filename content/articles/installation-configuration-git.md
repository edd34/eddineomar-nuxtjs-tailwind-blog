---
title: Git 101 ep1 - Installation et configuration initiale de Git
subtitle: Une série sur l'outil de version de contrôle Git
author: Eddine Omar
tags: git
date: 2022-06-08T18:00:00.00Z
draft: false
image: https://unsplash.com/photos/wX2L8L-fGeA/download?ixid=MnwxMjA3fDB8MXxhbGx8fHx8fHx8fHwxNjU5NzE1Nzc0&force=true&w=640
---
# Introduction
Git est un VCS (Version Control System) open source le plus populaire du marché. Si vous êtes un développeur, apprendre à utiliser Git est une compétence incontournable. J'utilise Git au quotidien depuis plusieurs années, et j'ai décidé de vous donner les éléments essentiels pour donner un élan à votre carrière.
 -

Nous allons voir au cours de cet article, comment installer et configurer Git.
Voici le sommaire de l'article :
1. Installation de Git sous Debian/Ubuntu/Linux Mint
2. Configuration intiale de Git

NB : je vais expliquer la marche à suivre si vous utiliser une distribution dérivée de Debian ou Ubuntu.

# 1. Installation de Git sous Debian/Ubuntu/Linux Mint
La première étape à effectuer est d'installer Git sur sa machine. Nous allons faire cela avec la ligne de commande :
```bash
sudo apt update && sudo apt upgrade
```

Pour vérifier l'installation de Git, on peut lancer sur la ligne de commande :
`git --version` ou `git --help` pour respectivement vérifier la version ou lire l'aide en ligne de commande de l'outil Git.

```bash
❯ git --version
git version 2.25.1
❯ git --help
usage : git [--version] [--help] [-C <chemin>] [-c <nom>=<valeur>]
           [--exec-path[=<chemin>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<chemin>] [--work-tree=<chemin>] [--namespace=<nom>]
           <commande> [<args>]

Ci-dessous les commandes Git habituelles dans diverses situations :

démarrer une zone de travail (voir aussi : git help tutorial)
   clone             Cloner un dépôt dans un nouveau répertoire
   init              Créer un dépôt Git vide ou réinitialiser un existant

travailler sur la modification actuelle (voir aussi : git help revisions)
   add               Ajouter le contenu de fichiers dans l'index
   mv                Déplacer ou renommer un fichier, un répertoire, ou un lien symbolique
   restore           Restaurer les fichiers l'arbre de travail
   rm                Supprimer des fichiers de la copie de travail et de l'index
   sparse-checkout   Initialiser et modifier l'extraction clairsemée

examiner l'historique et l'état (voir aussi : git help revisions)
   bisect            Trouver par recherche binaire la modification qui a introduit un bogue
   diff              Afficher les changements entre les validations, entre validation et copie de travail, etc
   grep              Afficher les lignes correspondant à un motif
   log               Afficher l'historique des validations
   show              Afficher différents types d'objets
   status            Afficher l'état de la copie de travail

agrandir, marquer et modifier votre historique
   branch            Lister, créer ou supprimer des branches
   commit            Enregistrer les modifications dans le dépôt
   merge             Fusionner deux ou plusieurs historiques de développement ensemble
   rebase            Réapplication des commits sur le sommet de l'autre base
   reset             Réinitialiser la HEAD courante à l'état spécifié
   switch            Basculer de branche
   tag               Créer, lister, supprimer ou vérifier un objet d'étiquette signé avec GPG

collaborer (voir aussi : git help workflows)
   fetch             Télécharger les objets et références depuis un autre dépôt
   pull              Rapatrier et intégrer un autre dépôt ou une branche locale
   push              Mettre à jour les références distantes ainsi que les objets associés

'git help -a' et 'git help -g' listent les sous-commandes disponibles et
quelques concepts. Voir 'git help <commande>' ou 'git help <concept>'
pour en lire plus à propos d'une commande spécifique ou d'un concept.
Voir 'git help git' pour un survol du système.
```

# 2. Configuration intiale de Git
La seconde étape à effectuer est de configurer l'outil git. Il faut savoir qu'un commit est constitué d'un auteur (qui comprend nom d'utilisateur et adresse email), d'une date, d'un hash et d'un commentaire.

Il convient au moment d'une installation fraîche de Git de configurer le nom d'utilisateur, l'adresse email et l'éditeur 
Il y a quelques éléments de configuration à prendre en compte :

 a. Configuration du nom d'utilisateur

 b. Configuration de l'adresse email

 c. Configuration de l'éditeur de texte (lors des conflits de merges ou lorsqu'il faut éditer une description )

## a. Configuration du nom d'utilisateur
Le nom d'utilisateur permet d'identifier l'auteur d'un commit à l'aide d'un pseudo ou nom d'utilisateur.
Pour configurer le nom d'utilisateur globalement, il faut taper la commande :
```bash
git config --global user.name "my_user_name"
```

Pour vérifier le nom d'utilisateur configuré :
```bash
❯ git config --global user.name
my_user_name
```

## b. Configuration de l'adresse email
L'adresse email permet de contacter au besoin l'auteur d'un commit (par mail).
Pour configurer l'adresse email globalement, il faut taper la commande :
```bash
git config --global user.email "username@example.com"
```

Pour vérifier le nom d'utilisateur configuré :
```bash
❯ git config --global user.email
username@example.com
```

## c. Configuration de l'éditeur de texte
L'éditeur de texte permet de modifier les commentaires de commits via le CLI ou un éditeur de texte graphique. Cela arrive lorsque l'on ammende un commit, lors de la résolution de conflits de merges, lors de l'ajout de commentaire pour un commit de merge etc...

L'éditeur de texte par défaut est `vi`, j'utilise `vim` personnellement. Il est également possible d'utiliser emacs ou un éditeur de texte en GUI comme vscode ou notepad++. Choisissez celui qui vous convient. Dans un environnement serveur, vous serez contraint d'utiliser un éditeur de texte dans le terminal.

Pour configurer l'éditeur de texte globalement, il faut taper la commande :
```bash
git config --global core.editor "vim"
```

Pour vérifier le nom d'utilisateur configuré :
```bash
❯ git config --global core.editor
vim
```

NB : cette étape est optionnelle.

# Conclusion
Maintenant que vous avez installé et configuré Git, nous verrons lors du prochain épisode comment intialiser un repo et créer vos premiers coommits.

# En savoir plus :
 - [Démarrage rapide - Installation de Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Installation-de-Git)
 - [Démarrage rapide - Paramétrage à la première utilisation de Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Param%C3%A9trage-%C3%A0-la-premi%C3%A8re-utilisation-de-Git)