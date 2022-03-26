<template>
  <div class="home">
    <FilterNav @filterChange="curFilter = $event" />
    <div v-if="projects.length">
      <div v-for="project in getFilterProjects" :key="project.id">
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
    getFilterProjects() {
      let filterProjects;
      if (this.curFilter == "completed") {
        filterProjects = this.projects.filter((project) => {
          return project.complete;
        });
      } else if (this.curFilter == "ongoing") {
        filterProjects = this.projects.filter((project) => {
          return !project.complete;
        });
      } else {
        filterProjects = this.projects;
      }
      return filterProjects;
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
