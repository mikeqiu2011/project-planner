<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="toggleShowDetail">
        {{ project.title }}
      </h3>
      <div class="icons">
        <span @click="toggleComplete" class="material-icons"> edit </span>
        <span @click="removeProject" class="material-icons"> delete </span>
        <span @click="toggleComplete" class="material-icons tick"> done </span>
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
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    toggleShowDetail() {
      this.showDetail = !this.showDetail;
    },
    toggleComplete() {
      // this.project.complete = !this.project.complete;
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }), //only send value this is changed
      })
        .then(this.$emit("complete", this.project.id))
        .catch((err) => console.log(err.message));
    },
    removeProject() {
      fetch(this.uri, { method: "DELETE" }) // first delete in db
        .then(() => this.$emit("remove", this.project.id)) // if success, delete it locally
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style scoped>
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
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
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
/* completed projects */
.project.complete {
  border-left: 4px solid #00ce89;
}
.project.complete .tick {
  color: #00ce89;
}
</style>