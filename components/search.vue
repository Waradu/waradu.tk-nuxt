<template>
  <div class="searchContainer">
    <div
      class="search"
      @keydown.enter="selectResult"
      @keydown.up="navigateResults(-1)"
      @keydown.down="navigateResults(1)"
    >
      <input
        ref="searchInput"
        type="text"
        v-model="searchQuery"
        placeholder="Search..."
        @input="search"
        @keydown.ctrl.75="toggleSearch"
        @keydown.cmd.75="toggleSearch"
      />
    </div>
    <div class="results" v-show="showResults">
      <ul>
        <li
          v-for="(result, index) in filteredResults"
          :key="result.title"
          :class="{ active: index === activeIndex }"
        >
          <a :href="result.link" @click="selectResult">
            <h3>{{ result.title }}</h3>
            <p>{{ result.subTitle }}</p>
          </a>
        </li>
      </ul>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  data() {
    return {
      searchQuery: "",
      searchResults: [
        {
          title: "TITLE 1",
          subTitle: "SUBTITLE 1",
          additinalSearchParameters: "help",
          link: "LINK 1",
        },
        {
          title: "TITLE 2",
          subTitle: "SUBTITLE 2",
          additinalSearchParameters: "",
          link: "LINK 2",
        },
        {
          title: "TITLE 3",
          subTitle: "SUBTITLE 3",
          additinalSearchParameters: "",
          link: "LINK 3",
        },
      ],
      showResults: false,
      activeIndex: -1,
    };
  },
  computed: {
    filteredResults() {
      const query = this.searchQuery.toLowerCase();
      if (query == "") {
        this.showResults = false
      }
      return this.searchResults.filter(
        (result) =>
          result.title.toLowerCase().includes(query) ||
          result.subTitle.toLowerCase().includes(query) ||
          result.additinalSearchParameters.toLowerCase().includes(query)
      );
    },
  },
  methods: {
    search() {
      this.showResults = true;
      this.activeIndex = -1;
    },
    selectResult() {
      if (
        this.activeIndex !== -1 &&
        this.activeIndex < this.filteredResults.length
      ) {
        const result = this.filteredResults[this.activeIndex];
        window.location.href = result.link;
      }
    },
    navigateResults(direction: number) {
      this.activeIndex =
        (this.activeIndex + direction + this.filteredResults.length) %
        this.filteredResults.length;
    },
    toggleSearch(event: KeyboardEvent) {
      if (event.ctrlKey || event.metaKey) {
        if (event.key === "k") {
          this.showResults = !this.showResults;
          if (this.showResults) {
            this.$nextTick(() => {
              this.$refs.searchInput.focus();
            });
          }
        }
      }
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
