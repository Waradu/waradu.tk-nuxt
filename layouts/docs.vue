<template>
  <button class="toggleThemeBtn material-symbols-rounded" @click="toggleTheme">
    dark_mode
  </button>
  <div class="container">
    <nuxt-link v-if="page.back_arrow" :to="getParentPath()" class="back-link">
      <span class="material-symbols-rounded icon_arrow_back">arrow_back</span
      ><span class="back-link-text">Zurück</span>
    </nuxt-link>
    <div class="header" :id="page.title.toLowerCase().replace(/\s+/g, '-')">
      <span class="title">{{ page.title }}</span><br />
      <span class="desc">{{ page.description }}</span>
    </div>
    <hr />
    <DocsContent :data="page.components" />
  </div>
</template>

<script lang="ts">
export default {
  props: {
    data: {
      type: Object,
      default: {},
    },
  },
  computed: {
    page(): Object {
      return this.data;
    },
    isRootRoute() {
      return this.$route.path === "/";
    },
  },
  methods: {
    toggleTheme() {
      const isDark =
        document.documentElement.getAttribute("data-theme") === "dark";
      const newTheme = isDark ? "light" : "dark";
      document.documentElement.setAttribute("data-theme", newTheme);
      localStorage.setItem("theme", newTheme);
    },
    getParentPath() {
      if (this.isRootRoute) {
        return "/";
      } else {
        const parentPath = this.$route.path.split("/").slice(0, -1).join("/");
        return parentPath;
      }
    },
  },
  mounted() {
    const theme = localStorage.getItem("theme");
    if (theme) {
      document.documentElement.setAttribute("data-theme", theme);
    }
  },
};
</script>

<style>
@import url("~/assets/css/docs.scss");
@import url("~/assets/global.css");
</style>