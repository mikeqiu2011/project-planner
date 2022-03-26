<template>
  <div>
    <form @submit.prevent="addProject">
      <label>Title</label>
      <input type="text" v-model="title" required />
      <label>Details</label>
      <textarea v-model="detail" required />
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      uri: "http://localhost:3000/projects",
      title: "",
      detail: "",
    };
  },
  methods: {
    addProject() {
      fetch(this.uri, {
        method: "POST",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
          complete: false,
        }),
      }).catch((err) => console.log(err));
    },
  },
};
</script>

<style>
</style>