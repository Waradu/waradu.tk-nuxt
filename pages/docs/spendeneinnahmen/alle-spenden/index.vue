<template>
  <NuxtLayout name="docs" :data="data"> </NuxtLayout>
</template>

<script lang="ts">
export default {
  data() {
    class Types {
      static get img() {
        return "normal";
      }

      static get stack() {
        return "stack";
      }

      static get space() {
        return "space";
      }

      static get text() {
        return "stack";
      }

      static get list() {
        return "list";
      }

      static get item() {
        return {
          normal: "normal",
          marked: "marked",
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
          { type: Types.stack, components: [{ type: Types.text, text: `Drücke als erstes beim Dashboard auf <span class="btn-bg">Spende erfassen</span>.` }] }
        ],
      },
    };
  },
};
</script>

<style>
/*  */
</style>
