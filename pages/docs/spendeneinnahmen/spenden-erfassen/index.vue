<template>
  <NuxtLayout name="docs" :data="data"> </NuxtLayout>
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
          normal: "normal list",
          marked: "marked list",
        };
      }
    }
    return {
      data: {
        title: `Spende Erfassen`,
        description: `Teile eingehende Spenden unter Personen, Projekte und Kampagnen auf.`,
        back_arrow: true,
        components: [
          { type: Types.img, src: `home.png` },
          {
            type: Types.text,
            text: `Drücke als erstes beim Dashboard auf <span class="btn-bg">Spende erfassen</span>.`,
          },
          { type: Types.space },
          { type: Types.img, src: `neue-spende.png` },
          { type: Types.text, text: `Füge als nächstes die Spende Daten ein.` },
          {
            type: Types.list,
            items: [
              { type: Types.item.normal, text: `Wann gespendet wurde.` },
              { type: Types.item.normal, text: `Wie viel gespendet wurde.` },
              {
                type: Types.item.normal,
                text: `Wer gespendet hat (Es werden automatisch Personen vorgeschlagen).`,
              },
              {
                type: Types.item.marked,
                text: `Um eine neue Person hinzuzufügen klicke auf "<span class="blue-text">Neue Spender/in erfassen</span>" und fülle die entsprechenden Daten der Person ein.`,
              },
              {
                type: Types.item.normal,
                text: `Von wo/Wegen was gespendet wurde.`,
              },
              { type: Types.item.normal, text: `Für was gespendet wurde.` },
            ],
          },
          {
            type: Types.text,
            text: `Klicke anschliessend auf <span class="btn-blue">Spende erstellen</span>.`,
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
