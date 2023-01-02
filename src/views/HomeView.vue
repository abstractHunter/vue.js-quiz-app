<template>
  <section>
    <h1>Welcome to Yellow Quizzes</h1>
    <div class="categories">
      <router-link
        v-for="category in categories"
        :to="'/quiz/' + category.slug"
        :key="category.id"
      >
        <div class="category">
          {{ category.name }}
          <p>{{ category.description }}</p>
        </div>
      </router-link>
    </div>
  </section>
</template>

<style>
h1 {
  text-align: center;
  margin: 2rem;
  color: #333;
}
.categories a {
  text-decoration: none;
  color: #333;
  font-size: larger;
}
.categories a p {
  font-size: smaller;
  color: #767;
}
.category {
  width: 500px;
  background-color: #f0f0f0;
  border: 2px solid #ccc;
  height: 50px;
  border-radius: 10px;
  margin: 2rem;
  padding: 1rem;
}
.category:hover {
  box-shadow: 0 0 20px #ccc;
}
</style>

<script>
import sourceData from "@/data.json";

export default {
  name: "HomeView",
  data() {
    return {
      categories: sourceData.categories,
    };
  },
};
</script>
