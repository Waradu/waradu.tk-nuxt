<template>
  <div class="generated-content">
    <template v-for="(component) in getData">
      <span v-if="component.type === 'text'" class="text" v-html="component.text"></span>
      <div v-if="component.type === 'space'" class="space"></div>
      <img v-if="component.type === 'img'" alt="image couldn't load" class="image" loading="lazy" :src="getImageSrc(component.src)" />
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
    page(): Object {
      return this.calc(this.data);
    },
    getData(): Object {
      return this.data;
    },
  },
  methods: {
    calc(content: Object) {
      var inner = "";
      var fullPath = this.$route.path;
      fullPath += fullPath.endsWith("/") ? "" : "/";
      var path = fullPath.split("/").slice(-2);
      fullPath = path[path.length - 2];

      class Types {
        static get img() {
          return "img";
        }

        static get space() {
          return "space";
        }

        static get text() {
          return "text";
        }

        static get list() {
          return "list";
        }

        static get item() {
          return {
            normal: "normal list",
            marked: "marked list",
          };
        }
      }

      class Templates {
        static img(src: String) {
          require(`~/assets/images/${fullPath}/${src}`)
          return `<img src="~/assets/images/${fullPath}/${src}" alt="image couldn't load" class="image" loading="lazy">`;
        }

        static text(text: String) {
          return `<span class="text">${text}</span>`;
        }

        static space() {
          return `<div class="space"></div>`;
        }

        static list(items: Array<{}>) {
          var list_content = "";
          items.forEach((item) => {
            if (item.type == Types.item.normal) {
              list_content += `<li class="list-text">${item.text}</li>`;
            } else if (item.type == Types.item.marked) {
              list_content += `<li class="list-text star">${item.text}</li>`;
            }
          });
          return `<ol class="list">${list_content}</ol>`;
        }
      }

      this.data.forEach((component) => {
        if (component.type == Types.img) {
          inner += Templates.img(component.src);
        } else if (component.type == Types.space) {
          inner += Templates.space();
        } else if (component.type == Types.text) {
          inner += Templates.text(component.text);
        } else if (component.type == Types.list) {
          inner += Templates.list(component.items);
        }
      });

      return inner;
    },
    getImageSrc(src) {
      var fullPath = this.$route.path;
      fullPath += fullPath.endsWith("/") ? "" : "/";
      var path = fullPath.split("/").slice(-2);
      fullPath = path[path.length - 2];
      return `/images/${fullPath}/${src}`;
    },
  },
};
</script>
