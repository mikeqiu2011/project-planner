<template>
  <h1 @click="toggleShowDetail">{{ project.title }}</h1>
  <p v-if="showDetail">{{ project.detail }}</p>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
    };
  },
  methods: {
    toggleShowDetail() {
      this.showDetail = !this.showDetail;
    },
  },
};
</script>

<style>
</style>