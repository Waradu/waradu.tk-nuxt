<template>
  <NuxtLayout name="paginator" :site="sites">
  </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    return {
      sites: [{ text: "Spendeneinnahmen", icon: "segment", link: "spenden-erfassen" }, { text: "Spendeneinnahmen", icon: "segment", link: "spenden-erfassen" }]
    };
  },
};
</script>

<style>
/* */
</style>