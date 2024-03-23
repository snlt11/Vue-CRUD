<template>
  <nav class="filter-nav">
    <button @click="filterBy('all')" :class="{ active: current === 'all' }">
      All
    </button>
    <button
      @click="filterBy('complete')"
      :class="{ active: current === 'complete' }"
    >
      Complete
    </button>
    <button
      @click="filterBy('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    filterBy(value) {
      this.$emit("filterValue", value);
    },
  },
};
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  outline: none;
  font-size: 10px;
  color: #8a8585;
  text-transform: uppercase;
  margin-right: 10px;
  font-weight: bold;
  cursor: pointer;
  letter-spacing: 1px;
}
button.active {
  color: hsla(160, 100%, 37%, 1);
}
</style>
