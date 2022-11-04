<template>
  <div>
    <header class="pt-16 pb-9 sm:pb-16 sm:text-center">
      <h1
        class="
          mb-4
          text-8xl
          sm:text-4xl
          tracking-tight
          text-slate-800
          font-extrabold
          dark:text-slate-200
        "
      >
        Blog
      </h1>
      <p class="text-lg text-slate-700 dark:text-slate-400">
        Tous les derniers articles en lien avec Python, Git, le développement
        logiciel, développement personnel pour les dev...
      </p>
    </header>
    <div class="space-y-16 mx-auto max-w-7xl">
      <blog-item
        v-for="article in articles"
        :key="article.title"
        :title="article.title"
        :description="article.description"
        :date="article.date"
        :slug="article.slug"
        :draft="article.draft"
      ></blog-item>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content("articles")
      .only([
        "title",
        "description",
        "img",
        "slug",
        "tag",
        "author",
        "date",
        "draft",
      ])
      .sortBy("date", "desc")
      .fetch();

    return {
      articles,
    };
  },
  head: {
    title: "🚀Eddine Omar - Lead dev Python / DevOps | Blogs 📰",
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content: "Bienvenue sur le devblog d'Eddine",
      },
    ],
    link: [
      {
        rel: "icon",
        type: "image/x-icon",
        href: "data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>💻</text></svg>",
      },
    ],
  },
};
</script>

<style></style>
