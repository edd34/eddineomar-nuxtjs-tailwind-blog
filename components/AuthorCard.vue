<template>
  <div class="md:fixed">
    <div class="md:block flex justify-center items-center">
      <nuxt-img
        :src="siteMetadata.author_image"
        loading="lazy"
        alt="me"
        class="shadow-xl md:h-60 md:w-60 h-40 w-40 rounded-full"
      />
      <div class="mb-2 mx-7 mt-4 justify-center items-center">
        <h1
          class="md:text-3xl text-2xl text-gray-800 font-bold dark:text-blue-100"
        >
          {{ siteMetadata.author }}
        </h1>
        <div class="md:text-lg text-gray-600 dark:text-blue-100">
          {{ siteMetadata.position }}
        </div>
        <div />
        <div class="md:text-lg text-gray-600 dark:text-blue-100">
          {{ siteMetadata.position2 }}
        </div>
        <div />
        <div class="md:text-lg text-gray-600 dark:text-blue-100">
          {{ siteMetadata.position3 }}
        </div>
        <br />
        <a
          :href="`mailto:${siteMetadata.email}`"
          class="text-gray-600 md:hidden mt-1 dark:text-blue-100"
        >
          {{ siteMetadata.email }}
        </a>
      </div>
    </div>

    <div class="mx-7 hidden md:block">
      <div class="my-2 text-gray-600 flex dark:text-blue-100">
        <Mail class="mr-1" />
        <a :href="`mailto:${siteMetadata.email}`"> {{ siteMetadata.email }}</a>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-100">
        <Glob class="mr-1" />
        <p>{{ siteMetadata.location }}</p>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-200">
        <Github class="mr-1" />
        <a :href="siteMetadata.github"> {{ siteMetadata.githubUser }}</a>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-200">
        <div class="mr-1" />
        <a
          href="http://www.catb.org/~esr/faqs/hacker-howto.html"
          target="_blank"
        >
          <i> How To Become A Hacker </i>
        </a>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-200">
        <div class="mr-1" />
        <a
          href="http://www.catb.org/~esr/faqs/smart-questions.html"
          target="_blank"
          download=""
        >
          <i> How to Ask Smart Questions </i>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Mail from "../assets/icon/mail.svg?inline";
import Glob from "../assets/icon/glob.svg?inline";
import Github from "../assets/icon/github_new.svg?inline";
import Malt from "../assets/icon/malt-logo.svg?inline";
import CV from "../assets/icon/file.svg?inline";
import siteMetaInfo from "@/data/sitemetainfo";
export default {
  components: { Mail, Glob, Github, CV, Malt },
  data: () => {
    return {
      siteMetadata: siteMetaInfo,
    };
  },
};
</script>
