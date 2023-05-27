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
        return "stack";
      }

      static get text() {
        return "stack";
      }

      static get list() {
        return {
          normal: "normal",
          marked: "marked",
        };
      }
    }
    return {
      data: {
        title: "TITLE",
        description: "DESCRIPTION",
        title_id: "TITLE_ID",
        back_arrow: true,
        components: [
          { type: Types.img, src: "home.png" },
          { type: Types.stack, components: [{ type: "text", text: "TEXT" }] },
          { type: Types.space },
          { type: Types.img, src: "neue-spende.png" },
          {
            type: Types.stack,
            components: [
              { type: Types.text, text: "TEXT" },
              {
                type: Types.list,
                items: [
                  { type: Types.list.normal, text: "TEXT" },
                  { type: Types.list.normal, text: "TEXT" },
                  { type: Types.list.normal, text: "TEXT" },
                  { type: Types.list.marked, text: "TEXT" },
                  { type: Types.list.normal, text: "TEXT" },
                  { type: Types.list.normal, text: "TEXT" },
                ],
              },
            ],
          },
        ],
      },
    };
  },
};
</script>

<style>
/*  */
</style>
