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
          return "stack";
        }

        static get text() {
          return "stack";
        }

        static get list() {
          return {
            normal: "normal",
            marked: "marked",
          };
        }
      }

      class Templates {
        static img(src: String) {
          return `<img src="/_nuxt/assets/images/home.png" alt="image couldn't load" class="image" loading="lazy">`;
        }

        static stack(stack: Array<{}>) {
          stack.forEach((stack_component) => {
            if (stack_component.type == Types.text) {
              inner += Templates.img(stack_component.src);
            }
          });
          return `<img src="/_nuxt/assets/images/home.png" alt="image couldn't load" class="image" loading="lazy">`;
        }
      }

      this.data.forEach((component) => {
        if (component.type == Types.img) {
          inner += Templates.img(component.src);
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
