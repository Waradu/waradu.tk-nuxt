<template>
  <div class="generated-content">
    <template v-for="(component) in getData">
      <span v-if="component.type === 'text'" class="text" v-html="component.text"></span>
      <div v-else-if="component.type === 'space'" class="space"></div>
      <img v-else-if="component.type === 'img'" alt="image couldn't load" class="image" loading="lazy" :src="getImageSrc(component.src)" />
      <ol v-else-if="component.type === 'list'" class="list">
        <template v-for="(item) in component.items">
          <li v-if="item.type === 'normal list'" class="list-text" v-html="item.text"></li>
          <li v-else-if="item.type === 'marked list'" class="list-text star" v-html="item.text"></li>
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
      var fullPath = this.$route.path;
      fullPath += fullPath.endsWith("/") ? "" : "/";
      var path = fullPath.split("/").slice(-2);
      fullPath = path[path.length - 2];
      return `/images/${fullPath}/${src}`;
    },
  },
  mounted() {
    console.log(this.data)
  },
};
</script>
