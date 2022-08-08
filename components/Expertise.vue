<template>
  <div class="mt-8">
    <div class="mt-2">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        Languages
      </h2>

      <ul class="flex flex-wrap gap-4 items-center">
        <li class="flex items-center">
          <Python class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <C class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <Cpp class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
      </ul>
    </div>
    <div class="mt-2">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        Bases de données
      </h2>

      <ul class="flex flex-wrap gap-4 items-center">
        <li class="flex items-center">
          <Mysql class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <Mongodb class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <Sqlite class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <Postgresql class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
        <li class="flex items-center">
          <Redis class="h-10 w-10 rounded-sm drop-shadow-sm" />
        </li>
      </ul>
    </div>
    <div class="mt-2">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        Frontend
      </h2>

      <ul class="flex flex-wrap gap-4 items-center">
        <li class="flex items-center">
          <Html class="h-10 w-10 rounded-sm drop-shadow-sm"></Html>
        </li>

        <li class="flex items-center">
          <Css class="h-10 w-10 rounded-sm drop-shadow-sm"></Css>
        </li>
        <!-- <li class="flex items-center">
          <Bootstrap class="h-10 w-10"></Bootstrap>
        </li>
        <li class="flex items-center">
          <TailwindCss class="h-10 w-10"></TailwindCss>
        </li> -->

        <li class="flex items-center">
          <Javascript class="h-10 w-10"></Javascript>
        </li>
        <li class="flex items-center">
          <Vuejs class="h-10 w-10"></Vuejs>
        </li>
        <li class="flex items-center">
          <Nuxt class="h-10 w-10"></Nuxt>
        </li>
        <Flutter class="h-10 w-10" />
      </ul>
    </div>
    <div class="mt-4">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        Backend
      </h2>
      <ul class="mb-6 flex flex-wrap gap-4">
        <li class="flex items-center">
          <Django class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Flask class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Solidity class="h-10 w-10" />
        </li>
      </ul>
    </div>
    <div class="mt-4">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        DevOps
      </h2>
      <ul class="mb-6 flex flex-wrap gap-4">
        <li class="flex items-center">
          <Git class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Github class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Gitlab class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Docker class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Linux class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Ubuntu class="h-10 w-10" />
        </li>
      </ul>
    </div>
    <div class="mt-4">
      <h2
        class="
          mb-2
          text-xl text-gray-700
          font-bold
          dark:text-blue-200
          capitalize
        "
      >
        Autre
      </h2>
      <ul class="mb-6 flex flex-wrap gap-4">
        <li class="flex items-center">
          <Vscode class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Markdown class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Npm class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Yarn class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Jira class="h-10 w-10" />
        </li>
        <li class="flex items-center">
          <Pandas class="h-10 w-10" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Javascript from "../assets/devicon/javascript.svg?inline";
import Html from "../assets/devicon/html.svg?inline";
import Css from "../assets/devicon/css.svg?inline";
import Vuejs from "../assets/devicon/vuejs.svg?inline";
import TailwindCss from "../assets/devicon/tailwindcss.svg?inline";
import Nuxt from "../assets/devicon/nuxt.svg?inline";
import Python from "../assets/devicon/python.svg?inline";
import Flutter from "../assets/devicon/flutter.svg?inline";
import Git from "../assets/devicon/git.svg?inline";
import Github from "../assets/devicon/github.svg?inline";
import Gitlab from "../assets/devicon/gitlab.svg?inline";
import C from "../assets/devicon/c.svg?inline";
import Django from "../assets/devicon/django.svg?inline";
import Flask from "../assets/devicon/flask.svg?inline";
import Java from "../assets/devicon/java.svg?inline";
import Mysql from "../assets/devicon/mysql.svg?inline";
import Mongodb from "../assets/devicon/mongodb.svg?inline";
import Solidity from "../assets/devicon/solidity.svg?inline";
import Sqlite from "../assets/devicon/sqlite.svg?inline";
import Vscode from "../assets/devicon/vscode.svg?inline";
import Cpp from "../assets/devicon/cpp.svg?inline";
import Docker from "../assets/devicon/docker.svg?inline";
import Linux from "../assets/devicon/linux.svg?inline";
import Markdown from "../assets/devicon/markdown.svg?inline";
import Npm from "../assets/devicon/npm.svg?inline";
import Postgresql from "../assets/devicon/postgresql.svg?inline";
import Yarn from "../assets/devicon/yarn.svg?inline";
import Ubuntu from "../assets/devicon/ubuntu.svg?inline";
import Jira from "../assets/devicon/jira.svg?inline";
import Pandas from "../assets/devicon/pandas.svg?inline";
import Redis from "../assets/devicon/redis.svg?inline";

export default {
  components: {
    Javascript,
    Html,
    Css,
    Vuejs,
    TailwindCss,
    Nuxt,
    Python,
    Flutter,
    Git,
    Github,
    C,
    Django,
    Flask,
    Gitlab,
    Java,
    Mysql,
    Mongodb,
    Solidity,
    Sqlite,
    Vscode,
    Cpp,
    Docker,
    Linux,
    Markdown,
    Npm,
    Postgresql,
    Yarn,
    Ubuntu,
    Jira,
    Pandas,
    Redis,
  },
};
</script>
