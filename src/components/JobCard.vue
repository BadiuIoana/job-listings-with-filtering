<script>
export default {
  components: {},
  props: {
    job: Object,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
<template>
  <div class="job-card-section" :class="{ isFeatured: job.featured }">
    <div class="description">
      <img :src="job.logo" alt="" />
      <div>
        <div class="company-and-labels">
          <p class="company">{{ job.company }}</p>
          <div class="labels-wrapper">
            <p v-if="job.new" class="label new">New!</p>
            <p v-if="job.featured" class="label featured">Featured!</p>
          </div>
        </div>
        <p class="position">{{ job.position }}</p>
        <div class="flex-wrapper">
          <p>{{ job.postedAt }}</p>
          <p>{{ job.contract }}</p>
          <p>{{ job.location }}</p>
        </div>
      </div>
    </div>
    <div class="categories">
      <button v-on:click="$emit('set-role-filter', job.role)">
        {{ job.role }}
      </button>
      <button v-on:click="$emit('set-level-filter', job.level)">
        {{ job.level }}
      </button>
      <button
        v-for="lang in job.languages"
        :key="lang"
        v-on:click="$emit('set-language-filter', lang)"
      >
        {{ lang }}
      </button>
      <button
        v-for="tool in job.tools"
        :key="tool"
        v-on:click="$emit('set-tool-filter', tool)"
      >
        {{ tool }}
      </button>
    </div>
  </div>
</template>
<style scoped>
.job-card-section {
  background: #ffffff;
  padding: 1rem;
  margin: 1rem 0 4rem 0;
  position: relative;
  display: block;
  box-shadow: 5px 5px 5px 5px #dfdfdf;
  border-radius: 0.3rem;
}
.job-card-section.isFeatured {
  border-left: 0.35rem solid var(--dark-cyan);
  border-top-left-radius: 0.3rem;
  border-bottom-left-radius: 0.3rem;
}

.job-card-section .description {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
}

.job-card-section img {
  height: 4rem;
  width: 4rem;
  position: absolute;
  top: -2rem;
}
.job-card-section .company-and-labels {
  display: flex;
  margin-top: 1rem;
  align-items: center;
}
.job-card-section .company-and-labels p.company {
  color: var(--dark-cyan);
  font-weight: 700;
  margin-right: 1rem;
}

.job-card-section .company-and-labels .labels-wrapper {
  display: flex;
  flex-wrap: nowrap;
  gap: 0.5rem;
}
.job-card-section .company-and-labels p.label {
  padding: 0.4rem 0.5rem 0.2rem 0.5rem;
  border-radius: 1.2rem;
  color: #ffffff;
  text-transform: uppercase;
  font-size: 12px;
}
.job-card-section .company-and-labels p.new {
  background: var(--dark-cyan);
}
.job-card-section .company-and-labels p.featured {
  background: var(--very-dark-gray-cyan);
}

.job-card-section .description p.position {
  margin: 0;
  font-weight: 700;
  font-size: 1.1rem;
}

.job-card-section .description .flex-wrapper {
  display: flex;
  justify-content: space-between;
  color: var(--dark-gray-cyan);
  max-width: 16rem;
}

.job-card-section .description .flex-wrapper p {
  position: relative;
}

.job-card-section .description .flex-wrapper p:after {
  content: "\2022";
  position: absolute;
  top: 50%;
  transform: translate(70%, -50%);
}

.job-card-section .description .flex-wrapper p:last-of-type:after {
  content: "";
}

.job-card-section .categories {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
.job-card-section .categories button {
  margin: 0;
  color: var(--dark-cyan);
  font-weight: 700;
  background: hsla(180, 29%, 50%, 0.2);
  padding: 0.2rem 0.4rem;
  border-radius: 0.3rem;
  border: none;
}

@media (min-width: 768px) {
  .job-card-section {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;
    margin-bottom: 1rem;
  }
  .job-card-section img {
    position: relative;
    top: 0;
  }

  .job-card-section .description {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 2rem;
  }
}
</style>