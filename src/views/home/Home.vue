<template>
  <!-- <div class="home">Home</div> -->
  <!-- <HomeNav /> -->
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <ProjectCard
        :project="project"
        @remove="handleRemove"
        @complete="handleComplete"
      />
    </div>
  </div>
  <div v-else>
    <p>Loading projects info...</p>
  </div>
</template>

<script>
import HomeNav from "./HomeNav.vue";
import ProjectCard from "../../../components/ProjectCard.vue";

export default {
  name: "Home",
  components: { HomeNav, ProjectCard },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((resp) => resp.json())
      .then((data) => {
        this.projects = data;
        console.log(this.projects);
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleRemove(id) {
      console.log("remove event catched by parent");
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      }); // not an inline function, have to reassign
      console.log(this.projects);
    },
    handleComplete(id) {
      project = this.projects.find((project) => project.id == id);
      project.complete = !project.complete;
      console.log(this.projects);
    },
  },
};
</script>
