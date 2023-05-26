<template>
  <nuxt-link to="../" class="link">
    <span class="material-symbols-rounded icon">arrow_back</span>
    <div class="text">Zurück</div>
  </nuxt-link>
  <ul>
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
      default: [{ text: "No info", icon: "question_mark", link: "N/A", na: true }],
    },
  },
  computed: {
    sites() {
      return this.site;
    },
  },
  methods: {
    getFullPath(relativePath: string) {
      const parentPath = this.$route.path;
      const fullPath = parentPath + '/' + relativePath;
      return fullPath;
    }
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
