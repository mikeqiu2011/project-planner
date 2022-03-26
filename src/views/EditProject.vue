<template>
  <div class="editproject" v-if="title">
    <form @submit.prevent="editProject">
      <label>Title</label>
      <input type="text" v-model="title" required />
      <label>Details</label>
      <textarea v-model="detail" required />
      <button>Update project</button>
    </form>
  </div>
  <div v-else>
    <p>Loading project info</p>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
      //   project: null,
      uri: "http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        // this.project = data;
        this.title = data.title;
        this.detail = data.detail;
        console.log(this.title);
      })
      .catch((err) => console.log(err));
  },
  methods: {
    editProject() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
        }),
      })
        .then(() => this.$router.push("/"))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
</style>