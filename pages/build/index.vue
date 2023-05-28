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
      <button class="themeToggle material-symbols-rounded bluebtn" @click="toggleTheme">
        dark_mode
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.text)"
      >
        text_fields
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.img)"
      >
        image
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.list)"
      >
        sort
      </button>
      <button
        class="add material-symbols-rounded"
        v-on:click="addEle(Elements.space)"
      >
        space_bar
      </button>
      <button
        class="download material-symbols-rounded greenbtn"
        @click="openImportPopup"
      >
        edit
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
  <button class="toggleTheme material-symbols-rounded" @click="toggleTheme">
    dark_mode
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

  <div class="import" id="import">
    <div class="import-content">
      <textarea
        id="importText"
        cols="30"
        rows="10"
        v-model="dataText"
      ></textarea>
      <button
        class="confirm material-symbols-rounded greenbtn"
        @click="closeImportPopup"
      >
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
          normal: "list item",
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
      dataText: "",
      isReloading: true
    };
  },
  computed: {
    previewData() {
      return this.data;
    },
  },
  mounted() {
    const theme = localStorage.getItem('theme');
    if (theme) {
      document.documentElement.setAttribute('data-theme', theme);
    }
    this.isReloading = false;
  },
  methods: {
    toggleTheme() {
      const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
      const newTheme = isDark ? 'light' : 'dark';
      document.documentElement.setAttribute('data-theme', newTheme);
      localStorage.setItem('theme', newTheme);
    },
    togglePage() {
      document.getElementById("builder").classList.toggle("showPreview");
    },
    toggleUI() {
      document.getElementById("builder").classList.toggle("hideUI");
    },
    downloadData() {
      this.data.back_arrow = true;
      const jsonData = JSON.stringify(this.data, null, 2);
      navigator.clipboard
        .writeText(jsonData)
        .then(() => {
        })
        .catch((error) => {
          console.error("Error copying data to clipboard:", error);
        });
      this.data.back_arrow = false;
    },
    clear() {
      this.data.components = [];
      this.data.title = ``;
      this.data.description = ``;
      this.closePopup();
    },
    openPopup() {
      document.getElementById("popup").style.display = "block";
    },
    closePopup() {
      document.getElementById("popup").style.display = "none";
    },
    openImportPopup() {
      document.getElementById("import").style.display = "block";
      this.dataText = JSON.stringify(this.data, null, 2);

      const obj = JSON.parse(jsonString);
    },
    closeImportPopup() {
      document.getElementById("import").style.display = "none";
      const obj = JSON.parse(this.dataText);
      this.data = obj
    },
    addEle(type) {
      this.data.components.push(type);
    },
  },
  head() {
    return {
      script: [
        {
          innerHTML: `
            (function() {
              const theme = localStorage.getItem('theme');
              document.documentElement.setAttribute('data-theme', theme || 'light');
            })()
          `
        }
      ]
    };
  }
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
