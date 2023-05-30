<template>
  <div class="searchContainer" v-if="!showSearch">
    <div class="searchInside">
      <div
        class="search"
        @keydown.enter="selectResult"
        @keydown.up="navigateResults(-1)"
        @keydown.down="navigateResults(1)"
      >
        <input
          ref="searchInput"
          class="searchBox"
          type="text"
          v-model="searchQuery"
          placeholder="Search..."
          @input="search"
        />
      </div>
      <div class="results">
        <div class="placeholder" v-show="!showResults">
          Search for pages or commands
        </div>
        <ul v-show="showResults" class="resultsUL">
          <li
            class="resultsLI"
            v-for="(result, index) in filteredResults"
            :key="result.title"
            :class="{ active: index === activeIndex }"
          >
            <a
              class="resultsLink"
              v-if="!result.command"
              :href="result.link"
              @click="selectResult"
            >
              <h3 class="resultsTitle">{{ result.title }}</h3>
              <p class="resultsDesc">{{ result.subTitle }}</p>
            </a>
            <div v-else @click="executeCommand(result.command)">
              <h3 class="resultsTitle">{{ result.title }}</h3>
              <p class="resultsDesc">{{ result.subTitle }}</p>
            </div>
          </li>
        </ul>
      </div>
      <div class="searchFooter">
        <div class="searchIconContainer">
          <div class="searchIcon">
            <svg width="15" height="15" aria-label="" role="img">
              <g
                fill="none"
                stroke="currentColor"
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="1.2"
              >
                <path d="M12 3.53088v3c0 1-1 2-2 2H4M7 11.53088l-3-3 3-3" />
              </g>
            </svg>
          </div>
          <div class="iconText">to select</div>
        </div>
        <div class="searchIconContainer">
          <div class="searchIcon">
            <svg width="15" height="15" aria-label="" role="img">
              <g
                fill="none"
                stroke="currentColor"
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="1.2"
              >
                <path d="M7.5 3.5v8M10.5 8.5l-3 3-3-3" />
              </g>
            </svg>
          </div>
          <div class="searchIcon">
            <svg width="15" height="15" aria-label="" role="img">
              <g
                fill="none"
                stroke="currentColor"
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="1.2"
              >
                <path d="M7.5 11.5v-8M10.5 6.5l-3-3-3 3" />
              </g>
            </svg>
          </div>
          <div class="iconText">to navigate</div>
        </div>
        <div class="searchIconContainer">
          <div class="searchIcon">
            <svg width="15" height="15" aria-label="" role="img">
              <g
                fill="none"
                stroke="currentColor"
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="1.2"
              >
                <path
                  d="M13.6167 8.936c-.1065.3583-.6883.962-1.4875.962-.7993 0-1.653-.9165-1.653-2.1258v-.5678c0-1.2548.7896-2.1016 1.653-2.1016.8634 0 1.3601.4778 1.4875 1.0724M9 6c-.1352-.4735-.7506-.9219-1.46-.8972-.7092.0246-1.344.57-1.344 1.2166s.4198.8812 1.3445.9805C8.465 7.3992 8.968 7.9337 9 8.5c.032.5663-.454 1.398-1.4595 1.398C6.6593 9.898 6 9 5.963 8.4851m-1.4748.5368c-.2635.5941-.8099.876-1.5443.876s-1.7073-.6248-1.7073-2.204v-.4603c0-1.0416.721-2.131 1.7073-2.131.9864 0 1.6425 1.031 1.5443 2.2492h-2.956"
                />
              </g>
            </svg>
          </div>
          <div class="iconText">to close</div>
        </div>
      </div>
    </div>
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
          additionalSearchParameters: "help",
          link: "LINK 1",
          command: "",
        },
        {
          title: "TITLE 2",
          subTitle: "SUBTITLE 2",
          additionalSearchParameters: "",
          link: "LINK 2",
          command: "",
        },
        {
          title: "Light/Dark Mode",
          subTitle: "Toggle light or dark mode",
          additionalSearchParameters: "dark light mode apperiance",
          link: "",
          command: "toggleTheme",
        },
      ],
      showResults: false,
      activeIndex: -1,
      showSearch: false,
    };
  },
  computed: {
    filteredResults() {
      const query = this.searchQuery.toLowerCase();
      if (query === "") {
        this.showResults = false;
      } else {
        this.showResults = true;
      }
      return this.searchResults.filter(
        (result) =>
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
      if (
        this.activeIndex !== -1 &&
        this.activeIndex < this.filteredResults.length
      ) {
        const result = this.filteredResults[this.activeIndex];
        if (result.command !== "") {
          this.executeCommand(result.command);
        } else {
          window.location.href = result.link;
        }
      }
    },
    navigateResults(direction: number) {
      event.preventDefault();
      this.activeIndex =
        (this.activeIndex + direction + this.filteredResults.length) %
        this.filteredResults.length;
    },
    executeCommand(command: string) {
      if (command == "toggleTheme") {
        const isDark =
          document.documentElement.getAttribute("data-theme") === "dark";
        const newTheme = isDark ? "light" : "dark";
        document.documentElement.setAttribute("data-theme", newTheme);
        localStorage.setItem("theme", newTheme);
      }
    },
  },
});
</script>

<style scoped>
@import url("~/assets/css/search.scss");
@import url("~/assets/global.scss");
</style>
