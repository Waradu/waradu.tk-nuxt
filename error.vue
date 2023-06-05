<template>
  <NuxtLayout name="error">
    <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 24 24" fill="none" stroke="currentColor"
      stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="moitor">
      <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
      <line x1="8" y1="21" x2="16" y2="21"></line>
      <line x1="12" y1="17" x2="12" y2="21"></line>
    </svg>
    
    <div class="inside-monitor">
      <div class="title" v-if="error.statusCode === 404">404</div>
      <div class="title" v-else>An error occurred - {{ error.statusCode }} </div>
      <NuxtLink class="toHome" to="/">Home</NuxtLink>
    </div>
  </NuxtLayout>
</template>

<script lang="ts">
export default {
  props: ['error'],
  computed: {
    referer() {
      return this.$route.query.referer || null;
    }
  }
}
</script>

<style scoped>
html, body, #__nuxt {
  display: grid !important;
  place-items: center !important;
}
.moitor {
  transition: .1s !important;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.inside-monitor {
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -100%;
  width: 300px;
  text-align: center;
}

.title {
  font-size: 80px;
  letter-spacing: 20px;
  font-weight: 800;
}

.toHome {
  font-size: 30px;
  color: var(--tx);
  text-decoration: underline !important;
  transform: color .2s;
}
</style>