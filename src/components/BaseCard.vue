<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg bg-white">
    <!-- <img class="w-full h-48 object-cover" :src="brewery.image" :alt="brewery.name"> -->
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{ brewery.name }}</div>
      <p class="text-gray-700 text-base">{{ brewery.brewery_type }}</p>
      <p class="text-gray-700 text-base">{{ brewery.phone }}</p>
      <a class="text-blue-500" :href="brewery.website_url" target="_blank">View Website</a>
    </div>
    <div class="px-6 pt-4 pb-2">
      <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{{
        brewery.country }}</span>
      <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{{
        brewery.city }}</span>
      <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{{
        brewery.state }}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'BaseCard',
    props: {
      brewery: {
        type: Object,
        required: true
      }
    }
  }
</script>