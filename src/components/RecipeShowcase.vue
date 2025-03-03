<template>
  <div class="recipe-showcase">
    <h1 class="text-3xl font-bold mb-4">Recipe Showcase</h1>
    <input 
      type="text" 
      v-model="searchQuery" 
      placeholder="Search for a recipe..." 
      class="mb-4 p-2 border border-gray-300 rounded" 
      aria-label="Search for a recipe"
    />
    <!-- Message for no results -->
    <div v-if="filteredRecipes.length === 0" class="text-center text-gray-500">
      <p>No recipes found</p>
    </div>
    <!-- Recipe grid display -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4" v-else>
      <div 
        v-for="(recipe, index) in filteredRecipes" 
        :key="index" 
        class="card bg-white rounded-lg shadow-md overflow-hidden" 
      >
        <!-- Display specific food image for each recipe -->
        <img
          class="object-cover h-[500px] w-full rounded-t-lg"  
          :src="foodImages[index]" 
          :alt="'A plate of ' + recipe.name"
          @error="onImageError(index)"
          loading="lazy"
        />
        <div class="p-4">
          <h2 class="font-bold text-lg">{{ recipe.name }}</h2>
          <p class="text-gray-700">{{ recipe.description || 'No description available.' }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { faker } from '@faker-js/faker';


const generateRecipes = () => {
  return Array.from({ length: 6 }, () => ({
    name: faker.food.dish(),
    description: faker.food.description(),
  }));
};


const foodImages = [
  'https://loremflickr.com/1280/800/food?random=1',  
  'https://loremflickr.com/1280/800/food?random=2',  
  'https://loremflickr.com/1280/800/dessert?random=3',  
  'https://loremflickr.com/1280/800/food?random=4',  
  'https://loremflickr.com/1280/800/food?random=5',  
  'https://loremflickr.com/1280/800/dessert?random=6',  
];

export default {
  data() {
    return {
      searchQuery: '',
      recipes: generateRecipes(),
      foodImages: foodImages,  
    };
  },
  computed: {
    filteredRecipes() {
      return this.recipes.filter(recipe =>
        recipe.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    // Handle errors in loading images
    onImageError(index) {
      // Fallback image if the current image fails to load or is invalid
      this.$set(this.foodImages, index, 'https://via.placeholder.com/1280x800.png?text=Image+Not+Available');
    },
  },
};
</script>

<style scoped>
.recipe-showcase {
  max-width: 1000px;  /* Increased max width to accommodate larger images */
  margin: auto;
  padding: 20px;
}

.card {
  transition: transform 0.2s;
  border: none;  /* Ensure no border is applied to cards */
}

.card:hover {
  transform: scale(1.05);  /* Slight scale on hover for interaction */
}

.object-cover {
  object-fit: cover; /* Adjusts image fitting to cover the area */
}
</style>
