<template>
  <ul>
    <li v-if="!(path == '/docs' || path == '/docs/')" class="item back">
      <nuxt-link :to="getParentPath()" class="link">
        <span class="material-symbols-rounded icon">arrow_back</span>
        <div class="text">Zurück</div>
      </nuxt-link>
    </li>
    <li class="item" v-for="site in sites" :class="{ na: site.na }">
      <nuxt-link :to="getFullPath(site.link)" class="link">
        <span class="material-symbols-rounded icon">{{ site.icon }}</span>
        <div class="text">{{ site.text }}</div>
      </nuxt-link>
    </li>
  </ul>
</template>

<script lang="ts">
export default {
  props: {
    site: {
      default: [
        { text: "No info", icon: "question_mark", link: "N/A", na: true },
      ],
    },
  },
  computed: {
    sites() {
      return this.site;
    },
    path() {
      return this.$route.path;
    },
    isRootRoute() {
      return this.$route.path === "/";
    },
  },
  methods: {
    getFullPath(relativePath: string) {
      var parentPath = this.$route.path;
      const slash = parentPath.endsWith("/") ? "" : "/";
      const fullPath = parentPath + slash + relativePath;
      return fullPath;
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
  mounted() {},
};
useHead({
  title: "Docs",
  link: [{ rel: "icon", type: "image/x-icon", href: "./docs.ico" }],
});
</script>

<style>
@import url("~/assets/css/paginator.scss");
@import url("~/assets/global.css");
</style>
