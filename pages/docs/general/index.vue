<template>
  <NuxtLayout name="docs" :data="data"></NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    class Types {
      static get img() {
        return "img";
      }

      static get space() {
        return "space";
      }

      static get text() {
        return "text";
      }

      static get list() {
        return "list";
      }

      static get item() {
        return {
          normal: "list item",
          marked: "marked list",
        };
      }
    }
    return {
      data: {},
    };
  },
};
</script>

<style>
/*  */
</style>
