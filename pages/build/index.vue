<template>
  <Head>
    <Title>ProDoc</Title>
    <link rel="shortcut icon" href="logo.ico" type="image/x-icon">
  </Head>
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
      <button title="Dark/Lightmode" class="themeToggle material-symbols-rounded bluebtn" @click="toggleTheme">
        dark_mode
      </button>
      <button title="Add Text" class="add material-symbols-rounded" v-on:click="addEle(Elements.text)">
        text_fields
      </button>
      <button title="Add Image" class="add material-symbols-rounded" v-on:click="addEle(Elements.img)">
        image
      </button>
      <button title="Add List" class="add material-symbols-rounded" v-on:click="addEle(Elements.list)">
        sort
      </button>
      <button title="Add Space" class="add material-symbols-rounded" v-on:click="addEle(Elements.space)">
        space_bar
      </button>
      <button title="Edit Data" class="download material-symbols-rounded greenbtn" @click="openImportPopup">
        edit
      </button>
      <button title="Clear all" class="clear material-symbols-rounded redbtn" @click="openPopup">
        clear
      </button>
    </div>
  </div>
  <div class="preview" id="preview">
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
      <button class="cancle material-symbols-rounded redbtn" @click="closePopup">
        clear
      </button>
      <button class="confirm material-symbols-rounded greenbtn" @click="clear">
        done
      </button>
    </div>
  </div>

  <div class="import" id="import">
    <div class="import-content">
      <textarea id="importText" cols="30" rows="10" v-model="dataText"></textarea>
      <button class="confirm material-symbols-rounded greenbtn" @click="closeImportPopup">
        done
      </button>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  watch: {
    data: {
      handler(newData) {
        localStorage.setItem("myData", JSON.stringify(newData));
      },
      deep: true,
    },
  },
  data() {
    class Elements {
      static get img() {
        return {
          type: "image",
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
          title: false,
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
        title: ``,
        description: ``,
        back_arrow: true,
        components: [],
      },
      dataText: "",
      isReloading: true,
    };
  },
  computed: {
    previewData() {
      return this.data;
    },
  },
  mounted() {
    const savedData = localStorage.getItem("myData");
    if (savedData) {
      this.data = JSON.parse(savedData);
    }

    const theme = localStorage.getItem("theme");
    if (theme) {
      document.documentElement.setAttribute("data-theme", theme);
    }

    this.isReloading = false;
  },
  methods: {
    toggleTheme() {
      const isDark =
        document.documentElement.getAttribute("data-theme") === "dark";
      const newTheme = isDark ? "light" : "dark";
      document.documentElement.setAttribute("data-theme", newTheme);
      localStorage.setItem("theme", newTheme);
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
        .then(() => { })
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
    },
    closeImportPopup() {
      document.getElementById("import").style.display = "none";
      const obj = JSON.parse(this.dataText);
      this.data = obj;
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
          `,
        },
      ],
    };
  },
};
</script>

<style scoped>
@import url("~/assets/css/build.scss");
@import url("~/assets/global.scss");
</style>
