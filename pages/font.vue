<template>
  <a href="/waradu-bold-rounded.ttf" class="font-grid" download="">
    <div class="stars">
      <svg
        class="sparkle"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M14.187 8.096L15 5.25L15.813 8.096C16.0231 8.83114 16.4171 9.50062 16.9577 10.0413C17.4984 10.5819 18.1679 10.9759 18.903 11.186L21.75 12L18.904 12.813C18.1689 13.0231 17.4994 13.4171 16.9587 13.9577C16.4181 14.4984 16.0241 15.1679 15.814 15.903L15 18.75L14.187 15.904C13.9769 15.1689 13.5829 14.4994 13.0423 13.9587C12.5016 13.4181 11.8321 13.0241 11.097 12.814L8.25 12L11.096 11.187C11.8311 10.9769 12.5006 10.5829 13.0413 10.0423C13.5819 9.50162 13.9759 8.83214 14.186 8.097L14.187 8.096Z"
          fill="black"
          stroke="black"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M6 14.25L5.741 15.285C5.59267 15.8785 5.28579 16.4206 4.85319 16.8532C4.42059 17.2858 3.87853 17.5927 3.285 17.741L2.25 18L3.285 18.259C3.87853 18.4073 4.42059 18.7142 4.85319 19.1468C5.28579 19.5794 5.59267 20.1215 5.741 20.715L6 21.75L6.259 20.715C6.40725 20.1216 6.71398 19.5796 7.14639 19.147C7.5788 18.7144 8.12065 18.4075 8.714 18.259L9.75 18L8.714 17.741C8.12065 17.5925 7.5788 17.2856 7.14639 16.853C6.71398 16.4204 6.40725 15.8784 6.259 15.285L6 14.25Z"
          fill="black"
          stroke="black"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M6.5 4L6.303 4.5915C6.24777 4.75718 6.15472 4.90774 6.03123 5.03123C5.90774 5.15472 5.75718 5.24777 5.5915 5.303L5 5.5L5.5915 5.697C5.75718 5.75223 5.90774 5.84528 6.03123 5.96877C6.15472 6.09226 6.24777 6.24282 6.303 6.4085L6.5 7L6.697 6.4085C6.75223 6.24282 6.84528 6.09226 6.96877 5.96877C7.09226 5.84528 7.24282 5.75223 7.4085 5.697L8 5.5L7.4085 5.303C7.24282 5.24777 7.09226 5.15472 6.96877 5.03123C6.84528 4.90774 6.75223 4.75718 6.697 4.5915L6.5 4Z"
          fill="black"
          stroke="black"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </div>
    <div class="font-big">W</div>
    <div class="name">Waradu Bold Rounded V1</div>
    <div class="abc">ABCDEFGHIJKLMNOPQRSTUVWXYZ</div>
    <div class="abc-lower">abcdefghijklmnopqrstuvwxyz</div>
    <div class="special">0123456789</div>
    <div class="arrows material-symbols-rounded">arrow_forward<span class="aa" style="margin-inline: 70px;"></span>arrow_back</div>
  </a>
</template>

<style lang="scss">
body,
html {
  height: 100%;
  overflow: hidden;
}

body {
  display: grid;
  place-items: center;
  --active: 0;
  background: hsl(260 calc(--active * 97%) 6%);
  transition: background var(--transition);
}

*,
*:after,
*:before {
  box-sizing: border-box;
  text-decoration: none;
}

:root {
  --transition: 0.25s;
  --spark: 1.8s;
}

body:has(.font-grid:is(:hover, :focus-visible)) {
  --active: 1;
}

.font-grid {
  cursor: pointer;
  user-select: none;
  position: relative;
  display: grid;
  place-items: center;
  border: 1px solid var(--search);
  border-radius: 20px;
  width: 600px;
  padding: 20px;
  grid-template-rows: 150px 30px 40px 30px 40px;
  text-align: center;

  --cut: 0.1em;
  --active: 0;
  --bg: radial-gradient(
      40% 50% at center 100%,
      hsl(270 calc(var(--active) * 97%) 72% / var(--active)),
      transparent
    ),
    radial-gradient(
      80% 100% at center 120%,
      hsl(260 calc(var(--active) * 97%) 70% / var(--active)),
      transparent
    ),
    hsl(260 calc(var(--active) * 97%) calc((var(--active) * 44%) + 12%));
  background: var(--bg);

  box-shadow: 0 0 calc(var(--active) * 6em) calc(var(--active) * 3em)
      hsl(260 97% 61% / 0.75),
    0 0.05em 0 0
      hsl(260 calc(var(--active) * 97%) calc((var(--active) * 50%) + 30%)) inset,
    0 -0.05em 0 0 hsl(260 calc(var(--active) * 97%) calc(var(--active) * 60%)) inset;
  transition: box-shadow var(--transition), scale var(--transition),
    background var(--transition);
  scale: calc(1 + (var(--active) * 0.1));

  * {
    font-family: waradu;
    letter-spacing: 3px;
    background: linear-gradient(
      90deg,
      hsl(0 0% calc((var(--active) * 100%) + 65%)),
      hsl(0 0% calc((var(--active) * 100%) + 26%))
    );
    -webkit-background-clip: text;
    color: transparent;
    transition: background var(--transition), filter var(--transition);
  }

  .name {
    font-size: 12px;
  }

  .font-big {
    font-size: 90px;
    letter-spacing: 0px;
    margin-left: 20px;
    cursor: pointer;
    z-index: 5;
  }

  .arrows {
    position: absolute;
    top: 65px;
    font-size: 50px !important;
    display: none;
  }
}

.font-grid:hover {
  filter: brightness(90%);
  --active: 1;
  .name {
    color: #cb9aff;
  }
}

.stars {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 50px;
  overflow: visible !important;
  transform-box: fill-box;
  transform-origin: center;

  .sparkle path:nth-of-type(1) {
    --scale: 0.5;
    --delay: 0.1;
    --base: 40%;
  }

  .sparkle path:nth-of-type(2) {
    --scale: 1.5;
    --delay: 0.2;
    --base: 20%;
  }

  .sparkle path:nth-of-type(3) {
    --scale: 2.5;
    --delay: 0.35;
    --base: 30%;
  }
  .sparkle {
    overflow: visible !important;

    path {
      transform-box: fill-box;
      transform-origin: center;
      transition: color var(--transition);
      animation-duration: 0.6s;
      animation-delay: calc((var(--transition) * 1.5) + (var(--delay) * 1s));
      color: hsl(0 0% calc((var(--active, 0) * 70%) + var(--base)));
      fill: currentColor;
      stroke: currentColor;
    }
  }
}

.font-grid:before {
  content: "";
  position: absolute;
  inset: -0.25em;
  z-index: -1;
  border: 0.25em solid hsl(260 97% 50% / 0.5);
  border-radius: 22px;
  opacity: var(--active, 0);
  transition: opacity var(--transition);
}

.font-grid:hover path {
  animation-name: bounce;
  color: white;
}

@keyframes bounce {
  35%,
  65% {
    scale: var(--scale);
  }
}

@keyframes float-out {
  to {
    rotate: 360deg;
  }
}

.aa {
  animation: 1s infinite alternate marin;
}

@keyframes marin {
  to {
    margin-inline: 50px;
  }
}
</style>
