<template>
  <div id="overlay"></div>
  <NuxtPage />
</template>

<style lang="scss">
@font-face {
  font-family: Inter;
  src: url("../assets/fonts/Inter.woff2") format("woff2");
  font-display: swap;
}

#overlay {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--bg);
  animation: fade 2s;
  animation-fill-mode: forwards;
}

@keyframes fade {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    display: none;
  }
}
</style>

<script lang="ts">
export default {
  mounted() {
    window.setInterval(() => {
      // @ts-ignore
      document.getElementById("overlay").style.display = "none";
    }, 2000);
  },
};
</script>