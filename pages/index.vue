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
      <div class="bigger th" style="--delay: .1s;">W</div>
      <div class="th" style="--delay: .2s;">A</div>
      <div class="th" style="--delay: .3s;">R</div>
      <div class="th" style="--delay: .4s;">A</div>
      <div class="th" style="--delay: .5s;">D</div>
      <div class="th" style="--delay: .6s;">U</div>
    </h1>
    <div class="text-container">
      <span class="p" style="--delay: .1s;">Developer,</span>
      <span class="p" style="--delay: .2s;">Gamer</span>
      <span class="p" style="--delay: .3s;">und</span>
      <span class="p" style="--delay: .5s;" id="random">3vTaL</span>
    </div>
    <div class="tags">
      <div class="tag" style="--delay: .1s;">html/css/js</div>
      <div class="tag" style="--delay: .2s;">minecraft</div>
      <div class="tag" style="--delay: .3s;">git</div>
      <div class="tag" style="--delay: .4s;">python</div>
      <div class="tag" style="--delay: .5s;">tauri/nuxt</div>
      <div class="tag center" style="--delay: .6s;"><div>...</div></div>
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
