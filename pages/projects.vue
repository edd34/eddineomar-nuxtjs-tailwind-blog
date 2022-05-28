<template>
  <div class="max-w-3xl px-4 mx-auto sm:px-6 xl:max-w-5xl xl:px-0">
    <div class="pt-6 pb-8 space-y-2 md:space-y-5">
      <h1
        class="
          text-3xl
          font-extrabold
          leading-9
          tracking-tight
          text-gray-900
          dark:text-gray-100
          sm:text-4xl sm:leading-10
          md:text-6xl md:leading-14
        "
      >
        Projets
      </h1>
      <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
        Parmis les projets dont j'ai réalisés ! Je travaille souvent avec
        Python, Django, Flask, Git, Github, Vue/Nuxt et TailwindCSS. Il y a
        également des projets cryptos avec web3py, solidity et plein d'autres à
        venir !
      </p>
      <p class="text-m leading-7 text-gray-500 dark:text-gray-400 italic">
        PSSST!? Au fait, ça vous dirait d'aller mettre des 🌟 dans mes projets
        perso sur Github ?
      </p>
    </div>
    <main class="relative mb-auto">
      <div class="">
        <div class="container py-12">
          <div class="flex flex-wrap -m-4">
            <project-card
              v-for="item in projectsData"
              :key="item.title"
              :title="item.title"
              :description="item.description"
              :href="item.href"
              :github="item.github"
              :tech1="item.tech1"
              :tech2="item.tech2"
              :tech3="item.tech3"
              :tech4="item.tech4"
            ></project-card>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import projectsData from "../data/projects";
export default {
  data() {
    return {
      projectsData: projectsData,
    };
  },
  head: {
    title: "🚀 Eddine OMAR | 🚧Projets🚧",
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content: "Quelques projets réalisés par Eddine OMAR",
      },
    ],
    link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
  },
};
</script>
