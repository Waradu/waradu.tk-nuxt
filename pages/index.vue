<template>
  <div class="test">
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
      <div class="bigger th">W</div>
      <div class="th">A</div>
      <div class="th">R</div>
      <div class="th">A</div>
      <div class="th">D</div>
      <div class="th">U</div>
    </h1>
    <div class="text-container">
      <p class="p">Developer, Gamer und</p>
      <p class="p" id="random">3vTaL</p>
    </div>
    <br />
    <div class="icons">
      <!-- <span class="material-symbols-rounded html">html</span>
			<span class="material-symbols-rounded css">css</span>
			<span class="material-symbols-rounded js">javascript</span> -->
      <a href="" class="material-symbols-rounded icon person"
        >person
        <div class="hover">About Me</div></a
      >
      <div class="icon-container">
        <div class="icon material-symbols-rounded">person</div>
        <div class="icon_hover">person</div>
      </div>
      <a href="" class="material-symbols-rounded icon code"
        >code
        <div class="hover">Projects</div></a
      >
      <a href="" class="material-symbols-rounded icon play_arrow"
        >play_arrow
        <div class="hover">My top animes</div></a
      >
      <a href="" class="material-symbols-rounded icon stadia_controller"
        >stadia_controller
        <div class="hover">Games I play</div></a
      >
      <a
        style="display: none"
        href=""
        class="material-symbols-rounded icon music_note"
        >music_note
        <div class="hover">Favorit Music</div></a
      >
      <a href="" class="material-symbols-rounded icon chat"
        >chat
        <div class="hover">Contact Me</div></a
      >
    </div>
  </div>
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
      document.getElementById("random").innerText = makeid(5);
    }, 80);
  },
};
</script>

<style>
@import url('~/assets/css/index.css');
</style>
