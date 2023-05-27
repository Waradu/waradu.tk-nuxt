<template>
  <div class="list-container">
    <div v-for="(item, index) in components" :key="item.id">
      <div
        class="draggable-item"
        :draggable="true"
        @dragstart="dragStart(index)"
        @dragover="dragOver(index)"
        @dragenter="dragEnter(index)"
        @drop="drop(index)"
      >
        <div v-if="index === dropIndex" class="drop-indicator"></div>
        <div class="component-type">{{ item.type }}</div>
        {{ item.text }}
      </div>
    </div>
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

<style scoped>
.list-container {
  display: grid;
  place-items: center;
}
.draggable-item {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-left: 4px solid black;
  cursor: grab;
  border-radius: 0px 12px 12px 0px;
  width: 500px;
  position: relative; /* Added */
}
.drop-indicator {
  position: absolute;
  top: -5px;
  left: -10px;
  width: calc(100% + 15px);
  height: calc(100% + 10px); /* Updated: Set height to 100% */
  border-radius: 4px 14px 14px 4px;
  background-color: #ff666650;
  z-index: 0;
  opacity: 0.5;
  pointer-events: none;
}
</style>
