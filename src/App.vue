<template>
  <div id="app">
    <user-profile></user-profile>
  </div>
</template>

<script>
import UserProfile from "./components/UserProfile.vue";

export default {
  name: "App",
  components: {
    UserProfile
  }
};
</script>

<style>
body{
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background: #f3f5fa;
}
</style>
