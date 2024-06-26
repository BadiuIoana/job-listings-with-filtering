<script >
import Header from "./components/Header.vue";
import Wrapper from "./components/Wrapper.vue";
import JobCard from "./components/JobCard.vue";
import Filters from "./components/Filters.vue";

export default {
  components: {
    Header,
    Wrapper,
    JobCard,
    Filters,
  },
  data() {
    return {
      jobs: [],
      jobsCopy: [],
      selectedFilters: {
        role: "",
        level: "",
        languages: [],
        tools: [],
      },
    };
  },
  methods: {
    setRoleFilter(role) {
      this.jobs = this.jobs.filter((job) => job.role == role);
      if (!this.selectedFilters.role) {
        this.selectedFilters = { ...this.selectedFilters, role: role };
      }
    },
    setLevelFilter(level) {
      this.jobs = this.jobs.filter((job) => job.level == level);

      if (!this.selectedFilters.level) {
        this.selectedFilters = { ...this.selectedFilters, level: level };
      }
    },
    setLanguageFilter(lang) {
      this.jobs = this.jobs.filter((job) =>
        job.languages.find((language) => language == lang)
      );
      if (!this.selectedFilters.languages.includes(lang)) {
        this.selectedFilters = {
          ...this.selectedFilters,
          languages: [...this.selectedFilters.languages, lang],
        };
      }
    },
    setToolFilter(tool) {
      this.jobs = this.jobs.filter((job) => job.tools.find((t) => t == tool));
      if (!this.selectedFilters.tools.includes(tool)) {
        this.selectedFilters = {
          ...this.selectedFilters,
          tools: [...this.selectedFilters.tools, tool],
        };
      }
    },
    resetRoleFilter() {
      this.jobs = this.jobsCopy;
      this.selectedFilters = { ...this.selectedFilters, role: "" };

      this.selectedFilters.level
        ? this.setLevelFilter(this.selectedFilters.level)
        : "";

      this.selectedFilters.languages.length > 0
        ? this.selectedFilters.languages.forEach((lang) =>
            this.setLanguageFilter(lang)
          )
        : [];

      this.selectedFilters.tools.length > 0
        ? this.selectedFilters.tools.forEach((tool) => this.setToolFilter(tool))
        : [];
    },
    resetLevelFilter() {
      this.jobs = this.jobsCopy;
      this.selectedFilters = { ...this.selectedFilters, level: "" };

      this.selectedFilters.role
        ? this.setRoleFilter(this.selectedFilters.role)
        : "";
      this.selectedFilters.languages.length > 0
        ? this.selectedFilters.languages.forEach((lang) =>
            this.setLanguageFilter(lang)
          )
        : [];
      this.selectedFilters.tools.length > 0
        ? this.selectedFilters.tools.forEach((tool) => this.setToolFilter(tool))
        : [];
    },
    resetLanguageFilter(lang) {
      this.jobs = this.jobsCopy;
      const languagesNewArray = this.selectedFilters.languages.filter(
        (language) => language !== lang
      );
      this.selectedFilters = {
        ...this.selectedFilters,
        languages: languagesNewArray,
      };
      this.selectedFilters.role
        ? this.setRoleFilter(this.selectedFilters.role)
        : "";
      this.selectedFilters.level
        ? this.setLevelFilter(this.selectedFilters.level)
        : "";

      this.selectedFilters.tools.length > 0
        ? this.selectedFilters.tools.forEach((tool) => this.setToolFilter(tool))
        : [];
      this.selectedFilters.languages.length > 0
        ? this.selectedFilters.languages.forEach((lang) =>
            this.setLanguageFilter(lang)
          )
        : [];
    },
    resetToolFilter(tool) {
      this.jobs = this.jobsCopy;
      const toolsNewArray = this.selectedFilters.tools.filter(
        (t) => t !== tool
      );
      this.selectedFilters = {
        ...this.selectedFilters,
        tools: toolsNewArray,
      };
      this.selectedFilters.role
        ? this.setRoleFilter(this.selectedFilters.role)
        : "";
      this.selectedFilters.level
        ? this.setLevelFilter(this.selectedFilters.level)
        : "";

      this.selectedFilters.tools.length > 0
        ? this.selectedFilters.tools.forEach((tool) => this.setToolFilter(tool))
        : [];
      this.selectedFilters.languages.length > 0
        ? this.selectedFilters.languages.forEach((lang) =>
            this.setLanguageFilter(lang)
          )
        : [];
      console.log(this.selectedFilters);
    },
    clearAllFilters() {
      this.jobs = this.jobsCopy;
      this.selectedFilters = {
        role: "",
        level: "",
        languages: [],
        tools: [],
      };
    },
  },
  created() {
    const getJobs = async () => {
      try {
        const response = await fetch("/src/assets/data/data.json");
        const data = await response.json();
        this.jobs = data;
        this.jobsCopy = data;
      } catch (error) {
        console.log(error.message);
      }
    };
    getJobs();
  },
};
</script>

<template>
  <section>
    <Header></Header>
    <Wrapper>
      <Filters
        :selectedFilters="selectedFilters"
        @reset-role-filter="resetRoleFilter"
        @reset-level-filter="resetLevelFilter"
        @reset-language-filter="resetLanguageFilter"
        @reset-tool-filter="resetToolFilter"
        @clear-all-filters="clearAllFilters"
      ></Filters>
      <div v-for="job in jobs" :key="job.id">
        <JobCard
          :job="job"
          @set-role-filter="setRoleFilter"
          @set-level-filter="setLevelFilter"
          @set-language-filter="setLanguageFilter"
          @set-tool-filter="setToolFilter"
        ></JobCard>
      </div>
    </Wrapper>
  </section>
</template>

<style scoped>
</style>
