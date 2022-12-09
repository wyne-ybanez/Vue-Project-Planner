<template>
  <nav class="filter-nav">
    <!-- Custom active class added based on the value 'current' holds -->
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View all
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
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
    // by argument refers to 'all', 'completed', 'ongoing'
    updateFilter(by) {
      this.$emit("filterChange", by); // we emit so the Home component can pick it up
    },
  },
};
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
