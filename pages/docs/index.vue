<template>
  <NuxtLayout name="paginator" :site="sites"> </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      sites: [
        {
          text: "Spendeneinnahmen",
          icon: "segment",
          link: "spendeneinnahmen",
          na: false,
        },
        {
          text: "Spendeneinnahmen",
          icon: "segment",
          link: "spendeneinnahmen",
          na: false,
        },
      ],
    };
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
