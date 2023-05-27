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
      <button class="add" v-on:click="addEle(Elements.text)">New Text</button>
      <button class="add" v-on:click="addEle(Elements.img)">New Img</button>
      <button class="add" v-on:click="addEle(Elements.space)">New Space</button>
      <button class="add" v-on:click="addEle(Elements.list)">New List</button>
      <button class="clear" @click="clear">Clear</button>
      <button class="download" @click="downloadData">Copy</button>
    </div>
  </div>
  <div class="preview">
    <NuxtLayout name="docs" :data="previewData" />
    <div class="previewText">Preview:</div>
  </div>
  <img class="w-img" src="~/assets/images/wrdu.png" />
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
    class Elements {
        static get img() {
          return {
            type: "img",
            src: ``,
          };
        }

        static get space() {
          return {
            type: "space",
          };
        }

        static get text() {
          return {
            type: "text",
            text: `NEW TEXT`,
          };
        }

        static get list() {
          return {
            type: "list",
            items: [],
          };
        }
      }
    return {
      Elements: Elements,
      data: {
        title: `Template`,
        description: `Template default decription`,
        back_arrow: false,
        components: [
          { type: Types.img, src: `home.png` },
          {
            type: Types.text,
            text: `Drücke als erstes beim Dashboard auf <span class="btn-bg">Spende erfassen</span>.`,
          },
          { type: Types.space },
          { type: Types.img, src: `neue-spende.png` },

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
    addEle(type) {
      this.data.components.push(type);
    },
  },
};
useHead({
  title: "Builder",
  link: [{ rel: "icon", type: "image/x-icon", href: "./docs.ico" }],
});
</script>

<style scoped>
@import url("~/assets/css/build.scss");
@import url("~/assets/global.css");
</style>
