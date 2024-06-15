<script setup>
import { ref, onMounted, computed } from 'vue';

import BaseCard from './components/BaseCard.vue';

import VueAwesomePaginate from 'vue-awesome-paginate';
// import Pagination from './components/Paginate.vue';
import Footer from './components/Footer.vue';

import axios from 'axios';

let breweriesHome = ref(new Set());

const itemsPerPage = ref(9);
const currentPage = ref(1);

const brewery_length = 50

onMounted(() => {
//   console.log("On Mount");
  axios.get('https://api.openbrewerydb.org/v1/breweries').then(response => {
    let allresponse = response.data;
    // let firstTwo = allresponse.slice(0, 3);
    // breweriesHome.value.add(allresponse);

    allresponse.forEach(brewery => {
      // console.log(brewery)
      breweriesHome.value.add(brewery);
    })
    
  });
});



</script>

<template>
    <div class="container mx-auto px-4">
      <h1 class="text-4xl font-bold text-center my-8"><a href="/">Breweries</a></h1>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <BaseCard v-for="brewery in breweriesHome" :key="brewery.id" :brewery="brewery" />
      </div>




      <Footer />
    </div>
  </template>