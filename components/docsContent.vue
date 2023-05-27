<template>
  <div v-html="page"></div>
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
  },
  methods: {
    calc(content: Object) {
      var inner = "";

      class Types {
        static get img() {
          return "normal";
        }

        static get stack() {
          return "stack";
        }

        static get space() {
          return "space";
        }

        static get text() {
          return "stack";
        }

        static get list() {
          return "list";
        }

        static get item() {
          return {
            normal: "normal",
            marked: "marked",
          };
        }
      }

      class Templates {
        static img(src: String) {
          return `<img src="/_nuxt/assets/images/${src}" alt="image couldn't load" class="image" loading="lazy">`;
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

        static stack(stack: Array<{}>) {
          var stack_content = "";
          stack.forEach((stack_component) => {
            if (stack_component.type == Types.text) {
              stack_content += Templates.text(stack_component.text);
            } else if (stack_component.type == Types.list) {
              stack_content += Templates.list(stack_component.items);
            }
          });
          return `<div class="text-container">${stack_content}</div>`;
        }
      }

      this.data.forEach((component) => {
        if (component.type == Types.img) {
          inner += Templates.img(component.src);
        } else if (component.type == Types.stack) {
          inner += Templates.stack(component.components);
        } else if (component.type == Types.space) {
          inner += Templates.space();
        }
      });

      return inner;
    },
    getAssetPath(src: String) {
      return `~/assets/images/${src}`;
    },
  },
};
</script>
