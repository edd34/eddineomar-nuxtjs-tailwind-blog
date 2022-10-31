---
title: "Release Python 3.11 : quoi de neuf ?"
description: "L'article qui fait peur aux développeurs le changelog suite à une nouvelle release de Python 🐍 !"
author: Eddine Omar
tags: google internet
date: 2022-10-31T10:00:00.00Z
draft: false
image: https://images.unsplash.com/photo-1538439907460-1596cafd4eff?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1156&q=80
---

L'article qui fait peur aux développeurs pour Halloween : le changelog suite à une nouvelle release de Python 🐍 !

🎉 La release 3.11 de Python est sortie il y a tout juste une semaine le 24 octobre 2022. Voici un récap des nouvelles features (non exhaustif) que je trouve super et qu'il vous faut essayer à tout prix :
- Localisation des erreurs plus précises dans des traces d'erreurs. Au lieu de simplement localiser la ligne qui contient une erreur, l'interpréteur va souligner dans la ligne, la variable ou la fonction erronée. En gros ce sont Blake et Mortimer qui vont vous dire exactement la cause du bug et pourquoi !
- Les exceptions peuvent être enrichies avec des notes. En levant une exception, rajouter des informations additionnelles sur le contexte de l'erreur. Top pour les tests !
- La librairie tomllib fait partie des librairies standards de Python (ne requiert plus l'installation de modules complémentaires pour lire ce format de fichier). Pour la culture, TOML est un format de fichier qui permet de décrire des configuration. Un peu comme YAML, JSON, .env mais cependant est un peu plus riche en fonctionnalité que ces trois derniers.
NB : la librairie TOML incluse ne permet que de lire les fichiers de configurations TOML pas de les écrires (donc d'en générer, bientôt peut-être). Go ici pour plus : https://toml.io/en/

Il est à noter que cette dernière version est 10 à 60% plus rapide que la précédente (3.10).

Le saviez-vous ? Les propositions d'amélioration du language Python sont définies dans des documents appelés PEP (pour Python Enhancement Proposals). Des vraies spec rédigées pour définir les évolutions du language.
Vosu avez surement entendues parler des EIP (Ethereum Improvements Proposals) pour la blockchain Etherum. Même concept ici avec Python.

Retrouvez la liste des PEP implémentés dans les releases notes officielles du language ici : https://lnkd.in/eezYdWnJ

Allez jeter un oeil, on ne sait jamais une feature peut régler un problème compliqué sur lequel vous bloquer depuis un moment.
Très formateurs et enrichissants de plonger dedans même si c'est cryptique par moment.

👍 Likez le post si vous avez des collègues qui travaillent en Python pour qu'ils en profitent et à la prochaine pour d'autres posts liés à Python !

PS : Je consacrerai quelques posts à l'avenir pour illustrer quelques PEP présentées dans cette nouvelle release (la pratique et l'action + la théorie > tout). Restez à l'affût !

#python #language #pep #computerscience #blockchain #news #release
