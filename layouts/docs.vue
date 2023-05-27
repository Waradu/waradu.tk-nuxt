<template>
  <div class="container">
    <nuxt-link :to="getParentPath()" class="back-link">
      <span class="material-symbols-rounded icon_arrow_back">arrow_back</span
      ><span class="back-link-text">Zurück</span>
    </nuxt-link>
    <div class="header" :id="page.title_id">
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
@import url("~/assets/css/docs.scss");
@import url("~/assets/global.css");
</style>