<template>
  <div class="home">
    <FilterNav @filterChange="curFilter = $event" :curFilter="curFilter" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
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
  </div>
</template>

<script>
import ProjectCard from "../components/ProjectCard.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  name: "Home",
  components: { ProjectCard, FilterNav },
  data() {
    return {
      projects: [],
      curFilter: "all",
    };
  },
  computed: {
    filteredProjects() {
      if (this.curFilter == "completed") {
        return this.projects.filter((project) => project.complete); //maping function
      }
      if (this.curFilter == "ongoing") {
        return this.projects.filter((project) => !project.complete);
      }
      return this.projects;
    },
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
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
      console.log(this.projects);
    },
    handleFilter(status) {
      console.log(status);
    },
  },
};
</script>
