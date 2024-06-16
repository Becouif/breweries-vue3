<script setup>
import { ref, onMounted, computed } from 'vue';
import BaseCard from './components/BaseCard.vue';
import Footer from './components/Footer.vue';
import axios from 'axios';

let breweriesHome = ref([]);

const brewery_length = 50;

onMounted(() => {
  axios.get('https://api.openbrewerydb.org/v1/breweries').then(response => {
    breweriesHome.value = response.data;
  });
});

// Pagination logic
let page = ref(1);
const perPage = 9;

const paginatedData = computed(() => {
  const start = (page.value - 1) * perPage;
  const end = page.value * perPage;
  return breweriesHome.value.slice(start, end);
});

const totalPages = computed(() => {
  return Math.ceil(breweriesHome.value.length / perPage);
});

const nextPage = () => {
  if (page.value < totalPages.value) {
    page.value += 1;
  }
};

const backPage = () => {
  if (page.value > 1) {
    page.value -= 1;
  }
};

const goToPage = (numPage) => {
  if (numPage >= 1 && numPage <= totalPages.value) {
    page.value = numPage;
  }
};
</script>

<template>
  <div class="container mx-auto px-4">
    <h1 class="text-4xl font-bold text-center my-8">
      <a href="/">Breweries</a>
    </h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <BaseCard v-for="brewery in paginatedData" :key="brewery.id" :brewery="brewery" />
    </div>
    <div class="flex justify-center my-4">
      <button 
        @click="backPage" 
        :disabled="page === 1" 
        class="mx-2 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700 disabled:bg-gray-300 disabled:cursor-not-allowed">
        Previous
      </button>
      <span class="mx-2">Page {{ page }} of {{ totalPages }}</span>
      <button 
        @click="nextPage" 
        :disabled="page === totalPages" 
        class="mx-2 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700 disabled:bg-gray-300 disabled:cursor-not-allowed">
        Next
      </button>
    </div>
    <Footer />
  </div>
</template>