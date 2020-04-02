<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Vue from "vue";
import Home from "./components/Home";

export default {
  name: "App",
  components: {
    Home
  }
};
</script>

<style>
#app {
  background-image: url("/assets/astronomy-1867616_1920.jpg");
  background-size: cover;
}
</style>
