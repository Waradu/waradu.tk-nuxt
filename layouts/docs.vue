<template>
  <div class="custom-element-example">
    <div class="title">
      {{ exampleTitle }}
    </div>
    <div class="page-content">
      <slot />
    </div>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    title: {
      type: String,
      default: null,
    },
  },
  computed: {
    exampleTitle() {
      return this.title || "Default Title";
    },
  },
  mounted() {},
};
</script>
