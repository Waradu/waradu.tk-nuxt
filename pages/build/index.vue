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
      <draggable v-model="data">
        <div v-for="item in data.components" :key="item.id">
          {{ item.text }}
        </div>
      </draggable>
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
import draggable from 'vuedraggable';

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
        title: `Template`,
        description: `Template default decription`,
        back_arrow: false,
        components: [
          { id: 1, text: "Item 1" },
          { id: 2, text: "Item 2" },
          { id: 3, text: "Item 3" },
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
            normal: "normal",
            marked: "marked",
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
