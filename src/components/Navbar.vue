<template>
  <nav class="main-nav">
    <router-link to="/">Projects</router-link>
    <router-link :to="{ name: 'addProject' }">Create Project </router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  font-size: 20px;
  border: 0;
  background: white;
}
a.router-link-active {
    border-bottom: 1px solid #00ce80;
    padding-bottom: 4px;
}
</style>
