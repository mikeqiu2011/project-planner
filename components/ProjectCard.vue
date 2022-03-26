<template>
  <h1 @click="toggleShowDetail" :class="{ complete: project.complete }">
    {{ project.title }}
  </h1>
  <button @click="toggleComplete">toggle complete</button>
  <button @click="remove">remove</button>
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
    toggleComplete() {
      this.project.complete = !this.project.complete;
    },
    remove() {
      this.$emit("remove");
      console.log("remove event emitted");
    },
  },
};
</script>

<style>
h1.complete {
  color: green;
}
</style>