<template>
  <div class="p-4 md:w-1/2 md" style="max-width: 544px">
    <div
      class="
        h-full
        overflow-hidden
        border-2 border-gray-200
        rounded-md
        border-opacity-60
        dark:border-gray-700
      "
    >
      <div class="p-6">
        <div class="flex flex-row justify-between items-center">
          <div class="my-2 flex flex-row items-center">
            <Folder class="w-8 h-8 mr-4 text-indigo-800" />
            <!-- <Python class="w-8 h-8 mr-4" /> -->
          </div>
          <div class="flex flex-row justify-between">
            <div class="mx-1">
              <a
                class="text-sm text-gray-500 transition hover:text-gray-600"
                target="_blank"
                rel="noopener noreferrer"
                :href="projectGithub"
                ><span class="sr-only">github</span
                ><img class="w-6 h-6" src="~assets/icon/github_new.svg"
              /></a>
            </div>
          </div>
        </div>
        <h2 class="text-2xl font-bold leading-8 tracking-tight mb-3">
          {{ projectTitle }}
        </h2>
        <p class="prose text-gray-500 max-w-none dark:text-gray-400 mb-3">
          {{ projectDescription }}
        </p>
        <div class="flex flex-row justify-between">
          <div class="text-black text-sm">
            {{ projectTech1 }} • {{ projectTech2 }} • {{ projectTech3 }} •
            {{ projectTech4 }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Folder from "../assets/icon/folder.svg?inline";
import Python from "../assets/devicon/python.svg?inline";
import Github from "../assets/icon/github.svg?inline";
export default {
  props: [
    "title",
    "description",
    "href",
    "github",
    "tech1",
    "tech2",
    "tech3",
    "tech4",
  ],
  components: { Folder, Github, Python },
  data() {
    return {
      projectTitle: this.title,
      projectDescription: this.description,
      projectHref: this.href,
      projectGithub: this.github,
      projectTech1: this.tech1,
      projectTech2: this.tech2,
      projectTech3: this.tech3,
      projectTech4: this.tech4,
    };
  },
};
</script>

<style></style>
