<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Details</label>
    <input type="text" v-model="detail" />
    <button>Edit</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects/" + this.id)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.title = data.title;
        this.detail = data.detail;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style></style>

