<template>
  <NuxtLayout name="paginator" :site="sites">
  </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      sites: [{ text: "Spendeneinnahmen", icon: "segment", link: this.getFullPath("erfassen") }, { text: "Spendeneinnahmen", icon: "segment", link: this.getFullPath("erfassen") }]
    };
  },
  methods: {
    getFullPath(relativePath: string) {
      const parentPath = this.$route.path;
      const fullPath = parentPath + '/' + relativePath;
      return fullPath;
    }
  },
  mounted() {
    console.log(this.sites)
  },
};
useHead({
  title: "Docs",
  link: [{ rel: "icon", type: "image/x-icon", href: "./docs.ico" }],
});
</script>

<style>
/* */
</style>