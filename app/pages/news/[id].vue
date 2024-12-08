<script setup lang="ts">
import { type News } from "../../../types/types";

const route = useRoute();
const { data } = await useFetch<News>(`https://fakestoreapi.com/products/${route.params.id}`);
if (data.value === undefined) {
  console.error('No data received from API');
}
</script>

<template>
  <div class="flex flex-col max-w-screen-lg container py-20 px-6">
    <!-- Header -->
    <div class="flex flex-col mb-8">
      <h2 class="text-4xl lg:text-5xl font-semibold text-gray-800 mb-4">{{ data?.title }}</h2>
    </div>
    <div class="relative mb-12">
      <NuxtImg
        :src="data?.image"
        densities="x1"
        sizes="xs:100vw sm:100vw md:100vw lg:100vw"
        class="w-full h-[400px] md:h-[500px] object-cover rounded-lg shadow-lg transition-transform duration-300 ease-in-out transform hover:scale-105"
        alt="News Image"
      />
      <div class="absolute top-0 left-0 w-full h-full bg-black opacity-30 rounded-lg"></div>
    </div>
    <div class="space-y-8">
      <h3 class="text-3xl font-semibold text-gray-800">More Details</h3>
      <p class="text-lg lg:text-xl text-gray-700">
      {{ data?.description }}
      <hr class="border-t-2 border-gray-200" />
      </p>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 90%;
}

h2, h3 {
  font-family: 'Roboto', sans-serif;
}

hr {
  margin-top: 16px;
  margin-bottom: 16px;
}

.relative {
  position: relative;
}

img:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

.text-gray-800 {
  color: #333;
}

.text-gray-600 {
  color: #4b5563;
}

.text-gray-700 {
  color: #374151;
}

.bg-black {
  background-color: rgba(0, 0, 0, 0.3);
}

.card-header {
  margin-bottom: 20px;
}

.card-title {
  font-size: 2rem;
  font-weight: bold;
}

.card-subtitle {
  font-size: 1.2rem;
  color: #888;
}
</style>
