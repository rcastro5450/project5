<template>
  <div id="app" class="bg-gray-100 min-h-screen flex items-center justify-center">
    <div class="container p-4">
      <!-- Recipe Showcase Component -->
      <RecipeShowcase />
    </div>
  </div>
</template>

<script>
// Import the RecipeShowcase component
import RecipeShowcase from './components/RecipeShowcase.vue';

export default {
  name: 'App',
  components: {
    RecipeShowcase,  // Register the RecipeShowcase component
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  text-align: center;
}

.container {
  max-width: 1200px;
  margin: auto;
}
</style>
