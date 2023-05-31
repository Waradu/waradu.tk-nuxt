<template>
  <NuxtPage />

  <Search v-if="getVar" @keydown.esc="showSearch = false" />
</template>

<script lang="ts">
export default {
  data() {
    return {
      showSearch: false,
    };
  },
  computed: {
    getVar() {
      return this.showSearch;
    },
  },
  methods: {
    handleKeyPress(event) {
      if (event.ctrlKey && event.key === "k") {
        event.preventDefault();
        this.showSearch = !this.showSearch;
        if (this.showSearch) {
          this.waitForFrame().then(() => {
            document.getElementById("searchInput")?.focus();
          });
        }
      } else if (event.key == "Escape") {
        this.showSearch = false;
      }
    },
    waitForFrame() {
      return new Promise((resolve) => {
        requestAnimationFrame(resolve);
      });
    },
  },
  mounted() {
    window.addEventListener("keydown", this.handleKeyPress);
  },
  beforeDestroy() {
    window.removeEventListener("keydown", this.handleKeyPress);
  },
};
</script>

<style lang="scss">
/*  */
</style>
