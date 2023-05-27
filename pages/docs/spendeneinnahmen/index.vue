<template>
  <NuxtLayout name="paginator" :site="sites">
  </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      sites: [
        {
          text: "Alle Spenden",
          icon: "apps",
          link: "alle-spenden",
          na: false,
        },
        {
          text: "Spende erfassen",
          icon: "add",
          link: "spenden-erfassen",
          na: false,
        },
        {
          text: "Zahlungen abgleichen",
          icon: "home",
          link: "spendeneinnahmen",
          na: true,
        },
        {
          text: "Spenden verdanken",
          icon: "person",
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
</script>

<style>
/* */
</style>