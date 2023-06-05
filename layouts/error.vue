<template>
  <button class="toggleThemeBtn material-symbols-rounded" @click="toggleTheme">
    dark_mode
  </button>
  <slot />
</template>

<script lang="ts">
export default {
  methods: {
    toggleTheme() {
      const isDark =
        document.documentElement.getAttribute("data-theme") === "dark";
      const newTheme = isDark ? "light" : "dark";
      document.documentElement.setAttribute("data-theme", newTheme);
      localStorage.setItem("theme", newTheme);
    },
  },
  mounted() {
    const theme = localStorage.getItem("theme");
    if (theme) {
      document.documentElement.setAttribute("data-theme", theme);
    }
  },
}
</script>

<style>
@import url("~/assets/css/paginator.scss");
@import url("~/assets/global.scss");
</style>