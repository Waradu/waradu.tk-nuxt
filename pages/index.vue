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
      <!--<span class="material-symbols-rounded html">html</span>
			<span class="material-symbols-rounded css">css</span>
			<span class="material-symbols-rounded js">javascript</span>-->
      <a href="" class="material-symbols-rounded icon person"
        >person
        <div class="hover">About Me</div></a
      >
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
:root {
  /*=======COLORS===========*/
  --bg: #16151a;
  --fg: #19181d;
  --e: #1c1b21;
  --tx: #85868b;
  --txb: #ffffff;
  --t: #e06c75;
  --search: #1e1d23;
}

@font-face {
  font-family: genshin;
  src: url("~/assets/fonts/zh-cn.ttf");
}

@font-face {
  font-family: Inter;
  src: url("~/assets/fonts/Inter.woff2");
}

* {
  border: 0;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Inter, sans-serif;
  color: var(--txb);
}

a {
  text-decoration: none;
  color: var(--txb);
}

.material-symbols-rounded {
  font-variation-settings: "FILL" 0, "wght" 400, "GRAD" 0, "opsz" 48;
  font-size: 30px !important;
  padding-inline: 5px;
  cursor: pointer;
}

body {
  height: 100vh;
  display: grid;
  place-items: center;
  background-color: var(--bg);
  overflow: hidden;
}

.test {
  display: grid;
  grid-template-columns: 200px 300px;
  grid-template-rows: 100px 40px 40px;
}

.img {
  width: 150px;
  grid-column: 1 / 2;
  grid-row: 1 / 4;
  transition: scale 0.5s;
}

.img:hover {
  scale: 1.03;
}

.h1 {
  cursor: pointer;
  color: var(--t);

  font-family: genshin;

  display: flex;
  align-self: end;
  font-size: 50px;
  font-weight: 700;
  grid-column: 2 / 3;
  grid-row: 1 / 2;
  line-height: 70px;

  background: linear-gradient(
      90deg,
      hsl(0, 90%, 65%),
      hsl(0.25turn, 90%, 65%),
      hsl(0.5turn, 90%, 65%),
      hsl(0.75turn, 90%, 65%),
      hsl(1turn, 90%, 65%),
      hsl(0.75turn, 90%, 65%),
      hsl(0.5turn, 90%, 65%),
      hsl(0.5turn, 90%, 65%),
      hsl(0.25turn, 90%, 65%),
      hsl(0, 90%, 65%)
    )
    0 0 / 800% 100%;
  -webkit-background-clip: text;
  background-clip: text;
  transition: 0.1s;
}

.th {
  font-family: genshin;
  color: var(--t);
  transition: 0.2s;
}

.th:hover {
  font-size: 60px;
  color: white;
}

.h1 > .bigger {
  margin-top: -7px;
  color: var(--t);
  font-family: genshin;
  font-size: 70px;
  transition: 0.2s;
}

.h1 > .bigger:hover {
  font-size: 80px;
  color: white;
  margin-left: -5px;
}

@keyframes move-bg {
  to {
    background-position: 800% 0;
  }
}

/*.h1:hover {
  color: transparent;
  animation: move-bg 30s infinite linear;
}*/

.text-container .p {
  margin-left: 5px;
  display: inline-block;
  font-size: 20px;
  font-weight: 300;
  font-family: "Inter", sans-serif;
  color: var(--tx);
}

.icons {
  display: flex;
  align-self: start;
  grid-column: 2 / 3;
  grid-row: 3 / 4;
}

.person:hover {
  transition: 0.2s;
  color: #27ae60;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}
.code:hover {
  transition: 0.2s;
  color: #9b59b6;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}
.play_arrow:hover {
  transition: 0.2s;
  color: #e74c3c;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}
.stadia_controller:hover {
  transition: 0.2s;
  color: #1abc9c;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}
.music_note:hover {
  transition: 0.2s;
  color: #f1c40f;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}
.chat:hover {
  transition: 0.2s;
  color: #d35400;
  animation: shake 0.5s 1;
  translate: 0px -5px;
}

.html:hover {
  transition: 0.2s;
  color: #e44d26;
  animation: shake 0.5s 1;
}
.js:hover {
  transition: 0.2s;
  color: #ffca28;
  animation: shake 0.5s 1;
}
.css:hover {
  transition: 0.2s;
  color: #42a5f5;
  animation: shake 0.5s 1;
}

@keyframes shake {
  0% {
    rotate: 0deg;
  }
  20% {
    rotate: 10deg;
  }
  40% {
    rotate: -10deg;
  }
  60% {
    rotate: 10deg;
  }
  80% {
    rotate: -10deg;
  }
  100% {
    rotate: 0deg;
  }
}

.hover {
  font-size: 12px;
  position: absolute;
  opacity: 0;
  color: var(--tx);
  background-color: var(--e);
  padding: 10px;
  border-radius: 4px;
  margin-top: 10px;
  transition: 0.2s;
}

.hover::before {
  content: "";
  position: absolute;
  top: -20%;
  left: 5px;
  width: 0;
  border-bottom: 10px solid var(--e);
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
}

.icon:hover > .hover {
  opacity: 1;
}
</style>
