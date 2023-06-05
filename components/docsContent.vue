<template>
  <div class="generated-content">
    <template v-for="component, index in getData">
      <span
        v-if="component.type === 'text'"
        class="text"
        :class="{ isTitle: component.title }"
        :id="encodeURIComponent(component.text)+`-${index}`"
        v-html="component.text"
      ></span>
      <div v-else-if="component.type === 'space'" class="space"></div>
      <img
        v-else-if="component.type === 'img'"
        alt="image couldn't load"
        class="image"
        loading="lazy"
        :src="getImageSrc(component.src)"
      />
      <ol v-else-if="component.type === 'list'" class="list">
        <template v-for="item in component.items">
          <li
            v-if="item.type === 'list item'"
            class="list-text"
            v-html="item.text"
          ></li>
          <li
            v-else-if="item.type === 'marked list'"
            class="list-text star"
            v-html="item.text"
          ></li>
        </template>
      </ol>
    </template>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    data: {
      type: Object,
      default: {},
    },
  },
  computed: {
    getData(): Object {
      return this.data;
    },
  },
  methods: {
    getImageSrc(src) {
      const validExtensions = ["png", "jpg", "jpeg", "gif", "webp"];

      var sub = src.split(".")[src.split(".").length-1]

      if (validExtensions.includes(sub) && (src.startsWith("http://") || src.startsWith("https://"))) {
        return src;
      }

      var fullPath = this.$route.path;
      fullPath += fullPath.endsWith("/") ? "" : "/";
      var path = fullPath.split("/").slice(-2);
      fullPath = path[path.length - 2];
      return `/images/${fullPath}/${src}`;
    },
  },
  mounted() {
  },
};
</script>
