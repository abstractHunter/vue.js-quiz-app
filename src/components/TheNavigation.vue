<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </nav>
</template>

<style>
nav {
  background-color: #bbb;
  padding: 1.4rem;
}

nav a {
  color: #333;
  text-decoration: none;
  margin: 1rem;
}

.active-link {
  font-weight: bold;
  color: #f56;
}
</style>

<script>
export default {
  name: "TheNavigation",
};
</script>
