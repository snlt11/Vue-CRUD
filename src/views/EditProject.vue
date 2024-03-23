<template>
  <h1>Edit Project</h1>
  <form @submit.prevent>
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Details</label>
    <input type="text" v-model="detail" />
    <button @click="updateProject">Update Project</button>
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
  methods: {
    updateProject() {
      fetch("http://localhost:3000/projects/" + this.id, {
        method: "PATCH",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
        }),
      })
        .then((response) => {
          this.$router.push("/");
        })
        .catch((error) => {
          return error.message;
        });
    },
  },
};
</script>

<style></style>
