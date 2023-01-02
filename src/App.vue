<template>
  <TheNavigation />
  <div class="container">
    <router-view />
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  font-family: "Roboto", sans-serif;
}

.container {
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 1rem;
}
</style>

<script>
import TheNavigation from "./components/TheNavigation.vue";
export default {
  name: "App",
  components: {
    TheNavigation,
  },
};
</script>
