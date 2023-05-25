<template>
  <div class="nav-container" :class="{ open: isNavbarOpen }">
    <div
      class="top-arrow"
      :class="{ rotated: isNavbarOpen, animate: animate }"
      @click="toggleNavbar"
    >
      expand_less
    </div>
    <input type="text" class="search-bar" id="search-bar" />
    <div class="quick-actions">
      <div class="nav-icon material-symbols-rounded active">person</div>
      <div class="nav-icon material-symbols-rounded">code</div>
      <div class="nav-icon material-symbols-rounded">handshake</div>
      <div class="nav-icon material-symbols-rounded">favorite</div>
      <div class="nav-icon material-symbols-rounded">link</div>
      <div class="nav-icon material-symbols-rounded">mail</div>
    </div>
    <div class="tabs">
      <div class="tab">
        <div class="tab-title">About Me</div>
        <div class="tab-content">
          <div class="tab-group">
            <div class="tab-group-title">Skills</div>
            <div class="tab-group-text"></div>
          </div>
          <div class="tab-group">
            <div class="tab-group-title">Freizeit</div>
            <div class="tab-group-text"></div>
          </div>
          <div class="tab-group">
            <div class="tab-group-title"></div>
            <div class="tab-group-text"></div>
          </div>
        </div>
      </div>
      <div class="tab">b</div>
      <div class="tab">c</div>
      <div class="tab">d</div>
      <div class="tab">e</div>
      <div class="tab">f</div>
    </div>
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
      animate: true,
    };
  },
  mounted() {
    this.setupNavbarInteraction();
  },
  methods: {
    setupNavbarInteraction() {
      var navContainer = document.querySelector(".nav-container");

      // @ts-ignore
      navContainer.addEventListener("mousedown", (event) => {
        // @ts-ignore
        this.startY = event.clientY;
        this.clicking = true;
      });

      document.addEventListener("mouseup", (event) => {
        this.startY = 0;
        this.clicking = false;
      });

      var main = this

      document.addEventListener("mousedown", (event) => {
        var navContainer = document.querySelector(".nav-container");
        var clickedElement = event.target;
        // @ts-ignore
        if (!navContainer.contains(clickedElement) && main.isNavbarOpen) {
          main.toggleNavbar()
        }
      });


      document.addEventListener("keydown", function (event) {
        if (event.ctrlKey && event.code === "Space") {
          main.toggleNavbar()
          if (main.isNavbarOpen) {
            // @ts-ignore
            document.getElementById("search-bar").focus()
          }
        }
      });

      // @ts-ignore
      navContainer.addEventListener("mousemove", (event) => {
        if (this.clicking) {
          // @ts-ignore
          var endY = event.clientY;
          var deltaY = this.startY - endY;

          if (deltaY > 30 || deltaY < -30) {
            this.toggleNavbar();
            this.clicking = false;
          }
        }
      });
    },
    toggleNavbar() {
      this.animate = false;
      this.isNavbarOpen = !this.isNavbarOpen;
    },
  },
};
</script>
