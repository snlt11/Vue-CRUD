<template>
  <h1>Create New Project</h1>
  <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title" />
    <label>Project Details</label>
    <input type="text" v-model="detail" />
    <button>Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  methods: {
    addProject() {
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
          complete: false,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
form {
  background-color: white;
  padding: 20px;
  border-radius: 20px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  margin: 20px 0 10px 0;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
}
input {
  padding: 10px;
  width: 100%;
  border: 0;
  border-bottom: 1px solid #ddd;
  box-sizing: border-box;
}
form button {
  margin: 20px auto 0;
  display: block;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
