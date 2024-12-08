<script setup lang="ts">
import { type News } from "../../types/types";
const {data, error} = await useFetch<News[]>("https://fakestoreapi.com/products");
</script>

<template>
  <main>
    <section class="py-20 container">
      <h2 class="text-3xl lg:text-5xl mb-6">Latest News Headlines</h2>
      <p class="text-lg lg:text-xl mb-8">Check out the top stories from around the globe!</p>
      
      <div v-if="!error" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 lg:gap-8">
        <div v-for="news in data" :key="news.id" class="flex flex-col bg-white rounded-lg shadow-xl overflow-hidden transition-transform transform hover:scale-105">
          <NuxtImg
            :src="news.image"
            sizes="xs:100vw sm:50vw lg:400px"
            format="webp"
            densities="x1"
            alt="News Image"
            class="w-full h-48 object-cover transition-all duration-300 ease-in-out hover:scale-110"
          />
          <div class="flex flex-col py-6 px-4 flex-1">
            <p class="text-xl lg:text-2xl font-semibold mb-2 text-gray-800">{{ news.title }}</p>
            <div class="text-lg lg:text-xl font-normal text-gray-600 mb-4 mt-auto">
              <span>{{ news.description.substring(0, 100) }} 
              <NuxtLink
              :to="`/news/${news.id}`"
              class="text-gray-800 font-semibold"
            >
              Read More
            </NuxtLink> ... </span>
            </div>
            
          </div>
        </div>
      </div>
      
      <p v-else class="text-xl text-center text-red-500">Oops, something went wrong. Please try again later.</p>
    </section>
  </main>
</template>

<style scoped>
/* Add the following styles to enhance the design of your cards */
.card {
  transition: transform 0.3s ease-in-out;
}

.card:hover {
  transform: translateY(-5px);
}

.card img {
  transition: transform 0.3s ease-in-out;
}

.card:hover img {
  transform: scale(1.05);
}

.card-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #333;
}

.card-description {
  color: #666;
  font-size: 1rem;
}

.card-button {
  background-color: #f79f1a;
  color: white;
  padding: 10px 15px;
  border-radius: 5px;
  text-align: center;
  cursor: pointer;
  text-decoration: none;
  margin-top: auto;
}

.card-button:hover {
  background-color: #f5a623;
  cursor: pointer;
}
</style>
