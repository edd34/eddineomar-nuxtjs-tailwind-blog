<template>
  <nav class="md:max-w-6xl mx-auto sticky top-0 z-50">
    <div
      class="
        bg-white
        flex flex-wrap
        items-center
        justify-center
        px-10
        md:py-4
        py-2
        overflow-hidden
        border-b border-gray-200
        font-2xl
        sm:px-4
        md:overflow-visible md:px-2
      "
    >
      <input class="menu-btn hidden" type="checkbox" id="menu-btn" />
      <label
        class="
          menu-icon
          block
          cursor-pointer
          md:hidden
          px-2
          relative
          select-none
        "
        for="menu-btn"
      >
        <span class="bg-grey-darkest flex items-center relative"></span>
      </label>

      <b-navbar>
        <template #start>
          <b-navbar-item
            v-for="elem in navLinks"
            :key="elem.path"
            :href="elem.path"
            :active="route_match(elem.path)"
          >
            <div v-if="route_match(elem.path)">
              <b class="is-active">{{ elem.name }}</b>
            </div>
            <div v-else>{{ elem.name }}</div>
          </b-navbar-item>
          <b-navbar-dropdown label="Boîte à outils">
            <b-navbar-item
              v-for="elem in navLinksTools"
              :key="elem.path"
              :href="elem.path"
              :active="route_match(elem.path)"
            >
              <div v-if="route_match(elem.path)">
                <b class="is-active">{{ elem.name }}</b>
              </div>
              <div v-else>{{ elem.name }}</div>
            </b-navbar-item>
          </b-navbar-dropdown>
        </template>
      </b-navbar>
    </div>
  </nav>
</template>

<script>
import menu from "../data/menu";

export default {
  name: "TheHeader",
  data() {
    return {
      navLinks: menu.menu,
      navLinksTools: menu.dropdown_menu_tools,
    };
  },
  methods: {
    route_match(param) {
      return param === this.$nuxt.$route.path;
    },
  },
};
</script>

<style>
.is-active {
  color: #4338ca;
}
/* .nuxt-link-exact-active {
} */
</style>
