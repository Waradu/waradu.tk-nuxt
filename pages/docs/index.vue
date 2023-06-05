<template>
  <NuxtLayout name="paginator" :site="sites"> </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      sites: [
        {
          text: "General",
          icon: "home",
          link: "general",
          na: false
        },
        {
          text: "Spendeneinnahmen",
          icon: "segment",
          link: "spendeneinnahmen",
          na: false,
        },
        {
          text: "Kampagne",
          icon: "home",
          link: "spendeneinnahmen",
          na: true,
        },
        {
          text: "Spender",
          icon: "person",
          link: "spendeneinnahmen",
          na: true,
        },
        {
          text: "Patenschaften",
          icon: "group",
          link: "spendeneinnahmen",
          na: true,
        },
        {
          text: "Mehr kommt noch",
          icon: "more_horiz",
          link: "spendeneinnahmen",
          na: true,
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
