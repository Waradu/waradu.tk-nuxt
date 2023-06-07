<template>
  <NuxtLayout name="docs" :data="data"> </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    class Types {
      static get img() {
        return "image";
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
      data: {
        title: `Alle Spenden`,
        description: `Teile eingehende Spenden unter Personen, Projekte und Kampagnen auf.`,
        back_arrow: true,
        components: [
          { type: Types.img, src: `home.png` },
          { type: Types.text, title: false, text: `Drücke als erstes beim Dashboard auf <span class="btn-bg">Spende erfassen</span>.` }
        ],
      },
    };
  },
};
</script>

<style>
/*  */
</style>
