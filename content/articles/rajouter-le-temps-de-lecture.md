---
title: Ajouter le temps de lecture d'un article de blog sur Nuxt
subtitle: La solution pour afficher le temps de lecture d'un article sur un site internet
category:
  - Architectures logicielles
author: Eddine Omar
date: 2022-05-20T18:00:00.00Z
draft: false
image: 
---

# Introduction

Avez-vous déjà remarqué l'indication du temps de lecture d'un article sur un site internet ? Vous êtes vous demandé comment cela est calculé ? Mais surtout comment l'insérer dans mon site internet Nuxt / Vue ?
Vous êtes au bon endroit, c'est justement ce que nous allons voir !

# Principe de calcul de temps de lecture

Alors pour faire simple, des chercheurs se sont un jour demandé comment mesurer le temps de lecture d'un texte ou article. Ils ont tout simplement demandé à beaucoup d'adultes de lire un texte d'un certain nombre de mot et ils les ont chronométré par la même occasion. De cette expérience, nous avons estimé environ **238 mots/minutes**. Valeur que nous allons utilisé pour la suite de notre développpement.

# Création d'un composant Vue
L'étape suivante est de créer un composant vue dans le dossier *components*.
Voici l'implémentation du composant :

**Fichier ReadingTime.vue**
```vue
<template>
  <span>Temps de lecture : {{ readingTime }} minutes</span>
</template>

<script>
export default {
  name: "readingTime",
  props: ["content"],
  computed: {
    readingTime() {
      let minutes = 0;
      const contentString = JSON.stringify(this.content);
      const words = contentString.split(" ").length;
      const wordsPerMinute = 238;
      minutes = Math.ceil(words / wordsPerMinute);
      return minutes;
    },
  },
};
</script>
```

**Fichier pages/blog/_slug.vue**
```vue
<reading-time
    :content="article.body"
    class="flex items-center font-medium mt-6 sm:mx-3 justify-center"
></reading-time>
```


Voici quelques remarques :
 * Pour compter le nombre de mots : on découpe l'article au niveau des caractères espace puis on récupère la taille du tableau résultant.
 * Pour calculer le nombre de minutes nécessaire : il faut diviser le nombre de mots de l'article par le nombre de par minutes. Ensuite on arrondit à l'entier supérieur.
 * Enfin on instancie le composant en mettant le contenu de l'article en paramètre du composant.

# Conclusion
On obtient un magnifique composant que l'on peut styliser mais qui permet d'estimer le temps de lecture. Il est bien évidemment possible de paramétrer le nombre de mots par minutes si on le souhaite. Notez que l'estimation du temps de lecture n'est pas très précise et variera d'un individu à un autre.
En espérant vous avoir appris quelque chose !

------------------------------------------

Sources :
* [https://mads.space/blog/adding-estimated-reading-time-to-my-blog-posts/](https://mads.space/blog/adding-estimated-reading-time-to-my-blog-posts/)

