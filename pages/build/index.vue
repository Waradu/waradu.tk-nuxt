<template>
  <div class="builder" id="builder">
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
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.text)"
      >
        addtext_fields
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.img)"
      >
        addimage
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.list)"
      >
        addsort
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.space)"
      >
        addspace_bar
      </button>
      <button
        class="download material-symbols-rounded greenbtn"
        @click="downloadData"
      >
        content_copy
      </button>
      <button class="clear material-symbols-rounded redbtn" @click="openPopup">
        clear
      </button>
    </div>
  </div>
  <div class="preview">
    <NuxtLayout name="docs" :data="previewData" />
    <div class="previewText">Preview:</div>
  </div>
  <button class="togglePage material-symbols-rounded" @click="togglePage">
    swap_horiz
  </button>
  <button class="toggleUI material-symbols-rounded" @click="toggleUI">
    fullscreen
  </button>
  <div class="popup" id="popup">
    <div class="popup-content">
      <div class="popup-text">Do you really want to clear EVERYTHING?</div>
      <button
        class="cancle material-symbols-rounded redbtn"
        @click="closePopup"
      >
        clear
      </button>
      <button class="confirm material-symbols-rounded greenbtn" @click="clear">
        done
      </button>
    </div>
  </div>
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
        description: `Template default description`,
        back_arrow: false,
        components: [
          {
            type: "text",
            text: "Empty",
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
    togglePage() {
      document.getElementById("builder").classList.toggle("showPreview");
    },
    toggleUI() {
      document.getElementById("builder").classList.toggle("hideUI");
    },
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
      this.data.components = [
        {
          type: "text",
          text: "Empty",
        },
      ];
      this.data.title = `Template`;
      this.data.description = `Template default decription`;
      this.closePopup();
    },
    openPopup() {
      document.getElementById("popup").style.display = "block";
    },
    closePopup() {
      document.getElementById("popup").style.display = "none";
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
