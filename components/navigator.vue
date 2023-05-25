<template>
  <div class="nav-container" :class="{ open: isNavbarOpen }">
    <div
      class="top-arrow animate"
      :class="{ rotated: isNavbarOpen, animate: animate }"
      @click="toggleNavbar"
    >
      expand_less
    </div>
    <div class="quick-actions">
      <div class="nav-icon">A</div>
      <div class="nav-icon">B</div>
      <div class="nav-icon">C</div>
      <div class="nav-icon">D</div>
      <div class="nav-icon">E</div>
      <div class="nav-icon">F</div>
    </div>
    <div class="other"></div>
  </div>
</template>

<style>
@import url("~/assets/css/navigator.scss");
</style>

<script lang="ts">
export default {
  data() {
    return {
      isNavbarOpen: false,
      startY: 0,
      clicking: false,
      animate: true
    };
  },
  mounted() {
    this.setupNavbarInteraction();
  },
  methods: {
    setupNavbarInteraction() {
      var navContainer = document.querySelector(".nav-container");

      // Handle swipe up gesture on the navbar
      navContainer.addEventListener("mousedown", (event) => {
        this.startY = event.clientY;
        this.clicking = true;
        console.log(this.clicking)
      });

      document.addEventListener("mouseup", (event) => {
        this.startY = 0
        this.clicking = false;
        console.log(this.clicking)
      });

      navContainer.addEventListener("mousemove", (event) => {
        if (this.clicking) {
          var endY = event.clientY;
          var deltaY = this.startY - endY;

          if (deltaY > 30 || deltaY < -30) {
            this.toggleNavbar();
            this.clicking = false
          }
        }
      });
    },
    toggleNavbar() {
      this.animate = false
      this.isNavbarOpen = !this.isNavbarOpen;
    },
  },
};
</script>
