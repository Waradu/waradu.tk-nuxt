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
          <div class="component-type">
            {{ item.type }}
            <input
              v-if="item.type === 'normal list' || item.type === 'marked list'"
              class="check-input"
              type="checkbox"
              :checked="item.type === 'marked list'"
              @change="handleCheckboxChange(index)"
            />
          </div>

          <div class="component-text" v-if="item.type == 'text'">
            <div class="edit-text">Text:</div>
            <input class="text-input" type="text" v-model="item.text" />
          </div>

          <div
            class="component-text"
            v-if="item.type == 'normal list' || item.type == 'marked list'"
          >
            <div class="edit-text">Text:</div>
            <input class="text-input" type="text" v-model="item.text" />
            
          </div>

          <div class="component-text" v-if="item.type == 'img'">
            <div class="edit-text">Src:</div>
            <input class="text-input" type="text" v-model="item.src" />
          </div>

          <div class="component-text" v-if="item.type == 'space'">
            Not editable
          </div>

          <div class="component-text" v-if="item.type == 'list'">
            <List :data="item.items" />
            <button class="add_to_list material-symbols-rounded greenbtn" @click="addItem(index)">add</button>
          </div>

          <div class="controlls">
            <button
              class="controll material-symbols-rounded"
              :disabled="index === 0"
              @click="moveItemUp(index)"
            >
              expand_less
            </button>
            <button
              class="controll material-symbols-rounded redbtn"
              @click="deleteItem(item, index)"
            >
              delete
            </button>
            <button
              class="controll material-symbols-rounded"
              :disabled="index === components.length - 1"
              @click="moveItemDown(index)"
            >
              expand_more
            </button>
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
      return this.data.components || this.data;
    },
  },
  data() {
    return {
      draggedIndex: null,
      dropIndex: null,
    };
  },
  methods: {
    handleCheckboxChange(index) {
      const item = this.components[index];
      item.type = item.type === 'marked list' ? 'normal list' : 'marked list';
    },
    addItem(index) {
      this.components[index].items.push(
        {
          type: "normal list",
          text: "Empty"
        }
      )
    },
    dragStart(index) {
      this.draggedIndex = index;
    },
    deleteItem(item, index) {
      if (item.type === 'list') {
        item.items.splice(index, 1);
      } else {
        this.components.splice(index, 1);
      }
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
    moveItemUp(index) {
      if (index > 0) {
        const currentItem = this.components[index];
        const previousItem = this.components[index - 1];
        this.components.splice(index - 1, 2, currentItem, previousItem);
      }
    },
    moveItemDown(index) {
      if (index < this.components.length - 1) {
        const currentItem = this.components[index];
        const nextItem = this.components[index + 1];
        this.components.splice(index, 2, nextItem, currentItem);
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import url("~/assets/css/list.scss");
@import url("~/assets/global.css");
</style>
