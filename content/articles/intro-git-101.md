---
title: Introduction série de blog Git 101
description: Une série sur l'outil de version de contrôle Git
author: Eddine Omar
tags: git
date: 2022-05-23T18:00:00.00Z
draft: false
image: https://unsplash.com/photos/KPAQpJYzH0Y/download?ixid=MnwxMjA3fDB8MXxhbGx8fHx8fHx8fHwxNjU5NzE1Njg4&force=true&w=640
---
# Introduction
En 2019, j'ai eu l'opportunité d'enseigner les rudiments du VCS Git à mes collègues lors d'un atelier pendant une mission de consulting chez un client. Je pense que cela profiterait à beaucoup plus de monde en retranscrivant ces ateliers dans une série de posts.

Je pense fortement que tous les développeurs sérieux devraient être à l'aise avec les rudiments des VCS, git étant le plus utilisé du marché. Les VCS sont parmis les outils indispensables dont ont besoin les développeurs de logiciels. Apprendre à maitriser un VCS comme Git vous donnera un avantage très dangereux par rapport à la concurrence.

Je me suis auto-formé sur Git depuis 2017, 5 ans au moment de l'écriture de cet article. Cela a principalement consisté en une pratique quotidienne dans les différentes entreprises et différents side-projects dont j'ai réalisé. Je suis suffisament à l'aide aujourd'hui pour partager ce savoir aujourd'hui.

Au cours de cette série de posts, je vais donner les bases de git ainsi que quelques techniques avancées.
Avant d'aller plus loin, rappelez vous que :
> devenir un développeur est un voyage et non une destination.


# Qu'est qu'un VCS ?
VCS signifie Version Control System, en français cela donne gestionnaire de version.

What is a VCS - Version Control System ?

"Les systèmes de contrôle de version sont une catégorie d'outils logiciels qui aident une équipe logicielle à gérer les modifications apportées au code source au fil du temps. Le logiciel de contrôle de version garde une trace de chaque modification du code dans un type spécial de base de données. En cas d'erreur, les développeurs peuvent se tourner remontez le temps et comparez les versions antérieures du code pour aider à corriger l'erreur tout en minimisant les perturbations pour tous les membres de l'équipe." [En savoir plus sur Atlassian.](https://www.atlassian.com/git/tutorials/what-is-version-control)

En termes simples, un VCS est comme un journal qui trace toutes les modifications qui ont lieu dans un code source : qui ? quelle ligne ? quand ? Il permet également de 

Git est le plus populaire VCS, il est opensource et a été crée par Linus Torvald, le créateur du célèbre kernel Linux.


# Ma première expérience avec le VCS Git

La première fois que j'ai utilisé Git dans un projet, c'était en 2017 lorsque nous avions un projet logiciel qui consistait à développer une application Android avec des spécifications. Le plus dur était que je n'avais jamais programmé en Java pour des smartphones Android : un nouveau langage de programmation, un autre paradigme et une autre méthodologie à acquérir, ainsi qu'une nouvelle façon de déboguer et de tester l'application. Donc le flux de développement était un peu chaotique au début, ma méthodologie fut la suivante :
 - réaliser le cahier des charges
 - apprendre comment développer une fonctionnalité précise
 - développer la fonctionnalité
 - tester et débugger
 - faire un commit lorsque je suis satisfait du développement effetué

Grâce à cela j'ai pu réaliser une belle démo de l'application, je n'aurais pas réussi sans Git.

Memorism est le nom du projet réalisé, il est hébergé sur Github à cette adresse : [https://github.com/edd34/memorism](https://github.com/edd34/memorism)

En versionnant votre projet, avez la possibilité de revenir en arrière, faire des commits dans des branches séparées et sécuriser votre développement.

# Quels sont les autres VCS sur le marché ?

Git n'est pas le seul VCS présent sur le marché, voici une liste non exhaustive de ses concurrents :
 - SVN : Apache Subversion est un VCS centralisé et opensource actuellement développé et maintenu par l'Apache Software Foundation et sa communauté.
 - Mercurial : est un VCS opensource et distribué, Matt Mackall en est le créateur en 2005.
 - Helix Core (avant Perforce Helic) : il s'agit d'un SVCS privé, maintenu et développé par Perforce Software, Inc depuis 1995.

Etc... Chaque VCS possède sa propre philosophie mais globalement ils effectuent la même taâche : vous aider à versionner, sécuriser votre logiciel et enregistrer tous les changements qui ont eu lieu au sein de celui-ci.


# Git vs SVN vs Mercurial vs Perforce
[Analyse Google Trends : Git vs SVN vs Mercurial vs Perforce](https://trends.google.com/trends/explore?geo=FR&q=git,svn,mercurial,perforce)

Nous pouvons voir que Git se démarque clairement de la concurrence. Cela est du à plusieurs facteurs à mon avis :
- Git est opensource et gratuit
- Git possède désormais une large communauté
- Git est un outil très puissant qui permet tous les types de workflow
- L'outil possède plusieurs GUI (client graphique) et est intégré à beaucoup (si ce n'est tous) les IDE populaire de nos jours

Bien que l'apprentissage de Git puisse sembler difficile au premier abord, je vous garantis qu'il s'agit d'un outil qui vous fera grandement avancer dans votre carrière de développeur professionnel.


Le plan de la série de billet de blog "Git 101" est le suivant :
- Partie 1 : Installation et configuration initiale de Git
- Partie 2 : Créer un repo local, création des premiers commits et historique.
- Partie 3 : Fonctionnalités avancées : branching et merging
- Partie 4 : Pourquoi et comment configurer une clé SSH dans Github
- Partie 5 : Comment contribuer à du code source dans Github ?
- Partie 6 : Comment gérer les conflits dans Git ?
- Partie 7 : L'arbre, l'index et le dépôt local.

Chaque point sera développé dans un article sur ce blog même. Restez à l'affût !
