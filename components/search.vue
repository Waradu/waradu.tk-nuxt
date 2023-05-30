<template>
  <div class="searchContainer">
    <div class="search" @keydown.enter="selectResult" @keydown.up="navigateResults(-1)" @keydown.down="navigateResults(1)">
      <input ref="searchInput" type="text" v-model="searchQuery" placeholder="Search..." @input="search" @keydown.ctrl.75="toggleSearch" @keydown.cmd.75="toggleSearch" />
    </div>
    <div class="results" v-show="showResults">
      <ul>
        <li v-for="(result, index) in filteredResults" :key="result.title" :class="{ active: index === activeIndex }">
          <a v-if="!result.command" :href="result.link" @click="selectResult">
            <h3>{{ result.title }}</h3>
            <p>{{ result.subTitle }}</p>
          </a>
          <div v-else @click="executeCommand(result.command)">
            <h3>{{ result.title }}</h3>
            <p>{{ result.subTitle }}</p>
          </div>
        </li>
      </ul>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  data() {
    return {
      searchQuery: '',
      searchResults: [
        {
          title: 'TITLE 1',
          subTitle: 'SUBTITLE 1',
          additionalSearchParameters: 'help',
          link: 'LINK 1',
          command: '',
        },
        {
          title: 'TITLE 2',
          subTitle: 'SUBTITLE 2',
          additionalSearchParameters: '',
          link: 'LINK 2',
          command: '',
        },
        {
          title: 'TITLE 3',
          subTitle: 'SUBTITLE 3',
          additionalSearchParameters: '',
          link: '',
          command: 'runCommand',
        },
      ],
      showResults: false,
      activeIndex: -1,
    };
  },
  computed: {
    filteredResults() {
      const query = this.searchQuery.toLowerCase();
      if (query === '') {
        this.showResults = false;
      } else {
        this.showResults = true;
      }
      return this.searchResults.filter(
        result =>
          result.title.toLowerCase().includes(query) ||
          result.subTitle.toLowerCase().includes(query) ||
          result.additionalSearchParameters.toLowerCase().includes(query)
      );
    },
  },
  methods: {
    search() {
      this.activeIndex = -1;
    },
    selectResult() {
      if (this.activeIndex !== -1 && this.activeIndex < this.filteredResults.length) {
        const result = this.filteredResults[this.activeIndex];
        if (result.command !== '') {
          this.executeCommand(result.command);
        } else {
          window.location.href = result.link;
        }
      }
    },
    navigateResults(direction: number) {
      this.activeIndex = (this.activeIndex + direction + this.filteredResults.length) % this.filteredResults.length;
    },
    toggleSearch(event: KeyboardEvent) {
      if (event.ctrlKey || event.metaKey) {
        if (event.key === 'k') {
          this.showResults = !this.showResults;
          if (this.showResults) {
            this.$nextTick(() => {
              this.$refs.searchInput.focus();
            });
          }
        }
      }
    },
    executeCommand(command: string) {
      console.log('Executing command:', command);
    },
  },
});
</script>

<style scoped>
@import url("~/assets/css/search.scss");
@import url("~/assets/global.scss");

.results .active {
  background-color: #f2f2f2;
}
</style>
