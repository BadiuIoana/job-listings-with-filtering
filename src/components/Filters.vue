<script>
export default {
  components: {},
  props: {
    selectedFilters: Object,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
<template>
  <div
    v-if="
      selectedFilters.role != '' ||
      selectedFilters.level != '' ||
      selectedFilters.languages.length != 0 ||
      selectedFilters.tools.length != 0
    "
    class="filter-section"
  >
    <ul class="filter-list">
      <li v-if="selectedFilters.role">
        {{ selectedFilters.role }}
        <button class="clear-filter" v-on:click="$emit('reset-role-filter')">
          <span>&#10005;</span>
        </button>
      </li>
      <li v-if="selectedFilters.level">
        {{ selectedFilters.level
        }}<button class="clear-filter" v-on:click="$emit('reset-level-filter')">
          <span>&#10005;</span>
        </button>
      </li>
      <li v-for="lang in selectedFilters.languages" :key="lang">
        {{ lang
        }}<button
          class="clear-filter"
          v-on:click="$emit('reset-language-filter', lang)"
        >
          <span>&#10005;</span>
        </button>
      </li>
      <li v-for="tool in selectedFilters.tools" :key="tool">
        {{ tool
        }}<button
          class="clear-filter"
          v-on:click="$emit('reset-tool-filter', tool)"
        >
          <span>&#10005;</span>
        </button>
      </li>
    </ul>
    <button class="clear-filters" v-on:click="$emit('clear-all-filters')">
      Clear all
    </button>
  </div>
</template>
<style scoped>
.filter-section {
  background: #ffffff;
  border-radius: 0.3rem;
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 3rem;
  padding: 0.5rem;
}
ul.filter-list {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  padding-left: inherit;
}

ul.filter-list li {
  margin: 0;
  color: var(--dark-cyan);
  font-weight: 700;
  background: hsla(180, 29%, 50%, 0.2);
  padding: 0.4rem;
  border-radius: 0.3rem;
  position: relative;
  border-top-right-radius: 0.2rem;
  border-bottom-right-radius: 0.2rem;
}

ul.filter-list button {
  position: absolute;
  right: 2px;
  transform: translate(100%, -50%);
  top: 50%;
  border: 0;
  border-top-right-radius: 0.2rem;
  border-bottom-right-radius: 0.2rem;
  padding: 0.4rem;

  background: var(--dark-cyan);
}
ul.filter-list button:hover {
  background: var(--very-dark-gray-cyan);
}
ul.filter-list button span {
  font-size: 12px;
  font-weight: 700;
  color: #ffffff;
  padding: 0;
}

button.clear-filters {
  border: none;
  background: none;
  color: var(--dark-cyan);
  font-weight: 700;
  text-decoration: underline;
  align-self: flex-start;
  font-size: 18px;
}

@media (min-width: 768px) {
  .filter-section[data-v-0ff34c05] {
    display: flex;
    flex-direction: row;
  }
  button.clear-filters[data-v-0ff34c05] {
    align-self: unset;
  }
}
</style>