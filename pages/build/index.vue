<template>
  <div class="builder">
    <div class="build-header">
      <div class="input-container">
        Title: <input class="text-input" type="text" v-model="data.title" />
      </div>
      <div class="input-container">
        Description:
        <input class="text-input" type="text" v-model="data.description" />
      </div>
    </div>
    <div class="build-content">
      <List :data="previewData" />
    </div>
    <div class="build-footer">
      <button v-on:click="addText">Add</button>
    </div>
  </div>
  <div class="preview">
    <NuxtLayout name="docs" :data="previewData" />
    <div class="previewText">Preview:</div>
  </div>
  <button class="clear" @click="clear">Clear</button>
  <button class="download" @click="downloadData">Copy</button>
  <img class="w-img" src="~/assets/images/wrdu.png" />
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
          normal: "normal list",
          marked: "marked list",
        };
      }
    }
    return {
      data: {
        title: `Template`,
        description: `Template default decription`,
        back_arrow: false,
        components: [
          { type: Types.img, src: `home.png` },
          {
            type: Types.stack,
            components: [
              {
                type: Types.text,
                text: `Drücke als erstes beim Dashboard auf <span class="btn-bg">Spende erfassen</span>.`,
              },
            ],
          },
          { type: Types.space },
          { type: Types.img, src: `neue-spende.png` },
          {
            type: Types.stack,
            components: [
              {
                type: Types.text,
                text: `Füge als nächstes die Spende Daten ein.`,
              },
              {
                type: Types.list,
                items: [
                  { type: Types.item.normal, text: `Wann gespendet wurde.` },
                  {
                    type: Types.item.normal,
                    text: `Wie viel gespendet wurde.`,
                  },
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
        ],
      },
    };
  },
  computed: {
    previewData() {
      return this.data;
    },
  },
  methods: {
    downloadData() {
      this.data.back_arrow = true;
      const jsonData = JSON.stringify(this.data, null, 2);
      console.log(jsonData);
      navigator.clipboard
        .writeText(jsonData)
        .then(() => {
          console.log("Data copied to clipboard");
        })
        .catch((error) => {
          console.error("Error copying data to clipboard:", error);
        });
      this.data.back_arrow = false;
    },
    clear() {
      this.data.components = [];
      this.data.title = `Template`;
      this.data.description = `Template default decription`;
    },
    addText() {
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
            normal: "normal list",
            marked: "marked list",
          };
        }
      }
      this.data.components.push({
        type: Types.stack,
        components: [
          {
            type: Types.text,
            text: `NEW TEXT`,
          },
        ],
      });
    },
  },
};
useHead({
  title: "Builder",
  link: [{ rel: "icon", type: "image/x-icon", href: "./docs.ico" }],
});
</script>

<style>
@import url("~/assets/css/build.scss");
@import url("~/assets/global.css");
</style>
