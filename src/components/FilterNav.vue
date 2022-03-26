<template>
  <nav class="filter-nav">
    <button
      @click="updateFilter('all')"
      :class="{ active: curFilter == 'all' }"
    >
      All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: curFilter == 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: curFilter == 'ongoing' }"
    >
      On going
    </button>
  </nav>
</template>

<script>
export default {
  props: ["curFilter"],
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
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