<template>
  <Navbar></Navbar>
  <RouterView />
</template>

<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: { Navbar },
};
</script>

<style></style>
