<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="flexing">
      <div>
        <h2 @click="showDetail = !showDetail">{{ project.title }}</h2>
      </div>
      <div>
        <span class="material-symbols-outlined" @click="deleteProject"
          >delete
        </span>
        <router-link :to="{ name: 'editProject', params: { id: project.id } }">
          <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span class="material-symbols-outlined" @click="completeProject">
          check
        </span>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
    <!-- {{ project.complete }} -->
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: "http://localhost:3000/projects/",
    };
  },
  methods: {
    deleteProject() {
      let deleteRoute = this.api + this.project.id;
      fetch(deleteRoute, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((error) => {});
    },
    completeProject() {
      let updateRoute = this.api + this.project.id;
      fetch(updateRoute, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then((response) => {
          this.$emit("complete", this.project.id);
        })
        .catch((error) => {
          console.log(error.Message);
        });
    },
  },
};
</script>

<style>
.project {
  padding: 20px;
  background-color: #f2f2f2;
  margin: 10px;
  border-left: 5px solid crimson;
  border-radius: 10px;
}
h2 {
  color: indigo;
  cursor: pointer;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
span {
  margin-left: 10px;
  color: #777;
}
span:hover {
  cursor: pointer;
  color: #777;
}
.complete {
  border-left-color: green;
}
</style>
