<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @filterValue="current = $event" :current="current"></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="deleteProject"
        @complete="completeProject"
      ></SingleProject>
    </div>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav.vue";
import SingleProject from "../components/SingleProject.vue";
export default {
  components: {
    FilterNav,
    SingleProject,
  },
  name: "Home",
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
  },

  computed: {
    filterProjects() {
      if (this.current === "complete") {
        return this.projects.filter((project) => {
          return project.complete;
        });
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => {
          return !project.complete;
        });
      }
      return this.projects;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.projects = data;
      })
      .catch((error) => {
        console.log(error.message());
      });
  },
};
</script>

<style></style>
