<template>
  <div class="list-container">
    <template v-for="(item, index) in components">
      <div
        class="draggable-item"
        :draggable="true"
        @dragstart="dragStart(index)"
        @dragover="dragOver(index)"
        @dragenter="dragEnter(index)"
        @drop="drop(index)"
      >
        <div class="di-inside">
          <div v-if="index === dropIndex" class="drop-indicator"></div>
          <div class="component-type">{{ item.type }}</div>
          
          <div class="component-text" v-if="item.type == 'text'">
            <div class="edit-text" >Text:</div>
            <input class="text-input" type="text" v-model="item.text" />
          </div>

          <div class="component-text" v-if="item.type == 'img'">
            <div class="edit-text" >Src:</div>
            <input class="text-input" type="text" v-model="item.src" />
          </div>
        </div>
      </div>
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
    components() {
      return this.data.components || [];
    },
  },
  data() {
    return {
      draggedIndex: null,
      dropIndex: null,
    };
  },
  methods: {
    dragStart(index) {
      this.draggedIndex = index;
    },
    drop(index) {
      const draggedItem = this.components[this.draggedIndex];
      this.components.splice(this.draggedIndex, 1);
      this.components.splice(index, 0, draggedItem);
      this.draggedIndex = null;
      this.dropIndex = null; // Reset dropIndex to hide the indicator
    },
    dragOver(index) {
      event.preventDefault();
      this.dropIndex = index;
    },
  },
};
</script>

<style scoped lang="scss">
@import url("~/assets/css/list.scss");
@import url("~/assets/global.css");
</style>
