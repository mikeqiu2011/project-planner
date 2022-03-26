<template>
  <div class="project">
    <div class="actions">
      <h3 @click="toggleShowDetail" :class="{ complete: project.complete }">
        {{ project.title }}
      </h3>
      <div class="icons">
        <span @click="toggleComplete" class="material-icons"> edit </span>
        <span @click="toggleComplete" class="material-icons"> delete </span>
        <span @click="toggleComplete" class="material-icons"> done </span>
      </div>
    </div>
    <div class="details">
      <p v-if="showDetail">{{ project.detail }}</p>
    </div>
  </div>

  <!-- <button @click="toggleComplete">toggle complete</button> -->
  <!-- <button @click="remove">remove</button> -->
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
.project {
  border-left: #e90074 solid 4px;
  background: white;
  margin: 20px auto;
  padding: 10px 20px;
  border-radius: 4px;
}
h3 {
  cursor: pointer;
}
.icons {
  cursor: pointer;
}
.actions {
  display: flex;
  align-items: center;
  justify-items: space-between;
}
</style>