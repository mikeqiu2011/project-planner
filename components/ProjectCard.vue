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

<style scoped>
h1.complete {
  color: green;
}
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
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
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
</style>