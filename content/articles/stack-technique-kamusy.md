---
title: "La stack technique de Kamusy"
description: "Voyons de quelles technologies Kamusy est constitué dans cet article"
author: Eddine Omar
tags: stack
date: 2022-08-10T18:00:00.00Z
draft: false
image: https://unsplash.com/photos/XJXWbfSo2f0/download?ixid=MnwxMjA3fDB8MXxzZWFyY2h8MXx8dGVjaG5vbG9neXxlbnwwfHx8fDE2NjAwODA3Njg&force=true&w=640
---
# Introduction
Dans cet article nous allons voir quelle est la stack technique du projet Kamusy, c'est-à-dire quelles sont les technologies qui ont permis de construire Kamusy.
À savoir, kamusy est une application fullstack (frontend + backend + base de donnée) construite sous une architecture microservice avec des technos moderne !

# Front
Le front ou client est la partie de l'application avec laquelle l'utilisateur va interagir directement. L'utilisateur appuiera sur les différents éléments d'interface qui sont entre autres les boutons, menus, liens hypertextes, listes déroulantes... Il saisira également des données dans les différents formulaires (formulaire de connexion, formulaire d'inscription, formulaire de recherche de mots...).

Un navigateur web moderne comprend le HTML (structure ou squelette de la page web), CSS (éléments visuels : formes, couleurs) et Javascript.
Écrire du code html, css, javascript fonctionnel et maintenable est relativement compliqué.
De nos jours (à partir des années 2010), avec la complexité et les besoins du web moderne, des frameworks frontend tels que Vue, Angular et React sont apparus pour faciliter la création d'application web moderne.

![Frontend desk development app](https://unsplash.com/photos/pKRNxEguRgM/download?ixid=MnwxMjA3fDB8MXxzZWFyY2h8Nnx8d2ViJTIwZGVzaWdufGVufDB8fHx8MTY2MDA4MTA3OQ&force=true&w=640)

La stack front de Kamusy est très classique. En voici les composants :
 - Framework web : VueJS
 - Appel API : axios
 - Store : Vuex
 - Routeur : Vue Router
 - Bibliothèque CSS : vuetify

# Backend
La partie backend également appelé partie serveur, permet de traiter des informations côté serveur et commniquer avec la base de données.
Un serveur est tout simplement un ordinateur distant qui exécute du code, des algorithmes, du calcul. Côté serveur, nous allons avoir du code qui s'exécute : ce code va récupérer les demandes, traiter, interpréter, éventuellement récupérer des données dans la base de données, calculer et renvoyer des informations à l'utilisateur sur le frontend mentionné plus haut.

De manière pratique, le frontend et le backend vont communiquer via un tunnel de communication appelé API. Le backend va récupérer des informations dans la base de données, faire un calcul avec ces données et renvoyer des informations traitées au frontend.

![server room](https://unsplash.com/photos/s0XabTAKvak/download?ixid=MnwxMjA3fDB8MXxzZWFyY2h8Mnx8c2VydmVyJTIwcm9vbXxlbnwwfHx8fDE2NjAwODU4NDY&force=true&w=640)

La stack de Kamusy est constituée des technologies suivantes :
 - Base de données : PostgreSQL
 - Cache : Redis
 - Framework backend : Django
 - Framework API : Django DRF
 - Language de programmation serveur : Python

# DevOps
Le DevOps peut être décrit comme l'unification du développement et de l'administration système. L'idée est de permettre aux développeurs d'avoir les outils pour mettre en production eux mêmes assez facilement.
Le DevOps contient les technologies de containerisation, les technologies d'infrastructure as a code et pas mal de chose as a code.

Personnellement je me sers beaucoup de Git et Github pour le versionning de mes projets. Docker et Docker-Compose sont incontournable tout au long du développement d'application fullstack car ils permettrent de reproduire le même environnement applicatif d'une machine de dev vers une machine de prod. Cela limite les effets de "ça marche sur mon ordi mais sur l'autre".
![server cables](https://unsplash.com/photos/zFYUsLk_50Y/download?ixid=MnwxMjA3fDB8MXxzZWFyY2h8MXx8c2VydmVyJTIwcm9vbXxlbnwwfHx8fDE2NjAwODU4NDY&force=true&w=640)

Dans la liste des outils DevOps, j'ai :
 - Git : permet de versionner le code source. Le code est hébergé sur Github.
 - Docker : Permet de containeriser des applications
 - Docker-Compose : permet d'organiser plusieurs containers dans des fichiers yml
 - Certbot SSL : permet de gérer les certificats HTTPS
 - Reverse-Proxy : permet de rediriger les requêtes front du front vers l'application côté serveur de manière sécurisée

Le déploiement se fait manuellement en appelant Git et les commandes docker-compose pour mettre à jour et relancer l'application.

# Autre
- Traitement et analyse de données : numpy et pandas
- Serveur web : nginx, http-server

# Conclusion
Une application web fullstack est composée de plusieurs technos. De plus on se sert de beaucoup d'outils comme les VCS pour faciliter le développement et le déploiement des applications.
Et vous, quels logiciels avez-vous déjà utilisé ou souhaitez-vous utiliser lors du développement de votre application fullstack ?
