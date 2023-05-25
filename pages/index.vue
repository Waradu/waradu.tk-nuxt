<template>
  <img class="bg" src="~/assets/svg/bg.svg">
  <div class="content-grid">
    <img
      src="~/assets/images/wrdu.png"
      alt=""
      class="img"
      data-tilt
      data-tilt-full-page-listening
      data-tilt-max="25"
      data-tilt-reverse="true"
    />
    <h1 class="h1">
      Waradu
    </h1>
    <div class="text-container">
      <span class="p" style="--delay: .1s;">Developer,</span>
      <span class="p" style="--delay: .2s;">Gamer</span>
      <span class="p" style="--delay: .3s;">und</span>
      <span class="p" style="--delay: .5s;" id="random">3vTaL</span>
    </div>
    <div class="tags">
      <div class="tag" style="--delay: .1s;">HTML/CSS/JS</div>
      <div class="tag" style="--delay: .2s;">MINECRAFT</div>
      <div class="tag" style="--delay: .3s;">GIT</div>
      <div class="tag" style="--delay: .4s;">PYTHON</div>
      <div class="tag" style="--delay: .5s;">TAURI/NUXT</div>
      <div class="tag" style="--delay: .6s;"><div>...</div></div>
    </div>
  </div>
  <navigator />
</template>

<script lang="ts">
import VanillaTilt from "~/assets/js/vt.js";

export default {
  head() {
    return {
      script: [
        {
          src: "~/assets/js/vt.js",
        },
      ],
    };
  },
  mounted() {
    VanillaTilt();

    function makeid(length: number) {
      let result = "";
      const characters =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
      const charactersLength = characters.length;
      let counter = 0;
      while (counter < length) {
        result += characters.charAt(
          Math.floor(Math.random() * charactersLength)
        );
        counter += 1;
      }
      return result;
    }
    window.setInterval(() => {
      // @ts-ignore
      document.getElementById("random").innerText = makeid(5);
    }, 80);
  },
};
</script>

<style>
@import url("~/assets/css/index.scss");
</style>
