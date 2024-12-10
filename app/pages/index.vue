<script setup lang="ts">
import {type News} from '../../types/types';
const loading = ref(true);
const data = ref();
const errorOccured = ref(false);
const searchNews = ref('');
const filteredNews = ref<News[]>([]);
const currentPage = ref(1);
const itemsPerPage = 8;

async function getNews() {
  const {data: apiData, error} = await useFetch<News[]>(
    'https://fakestoreapi.com/products'
  );

  if (apiData.value) {
    data.value = apiData.value;
    filteredNews.value = apiData.value.slice(0, itemsPerPage);
  }
  if (error.value) {
    errorOccured.value = true;
  }
  loading.value = false;
}

watchEffect(() => {
  getNews();
});

watch(
  () => searchNews.value,
  () => {
    if (!searchNews.value) {
      filteredNews.value = data.value.slice(0, itemsPerPage);
    } else {
      const results = data.value.filter((news: News) =>
        news.title.toLowerCase().includes(searchNews.value.toLowerCase())
      );
      filteredNews.value = results.slice(0, itemsPerPage);
    }
    currentPage.value = 1;
  }
);
watch(
  () => currentPage.value,
  () => {
    const start = (currentPage.value - 1) * itemsPerPage;
    const end = start + itemsPerPage;
    filteredNews.value = searchNews.value
      ? data.value
          .filter((news: News) =>
            news.title.toLowerCase().includes(searchNews.value.toLowerCase())
          )
          .slice(start, end)
      : data.value.slice(start, end);
  }
);
</script>

<template>
  <main>
    <section class="py-20 container">
      <h2 class="text-3xl lg:text-5xl mb-6">Latest News Headlines</h2>
      <p class="text-lg lg:text-xl mb-8">
        Check out the top stories from around the globe!
      </p>
      <div class="mb-6">
        <input
          v-model="searchNews"
          type="text"
          placeholder="Search news..."
          class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
      </div>
      <div v-if="loading">
        Loading...
      </div>
      <div
        v-if="!errorOccured"
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 lg:gap-8"
      >
        <div
          v-for="news in filteredNews"
          :key="news.id"
          class="flex flex-col bg-white rounded-lg shadow-xl overflow-hidden transition-transform transform hover:scale-105"
        >
          <NuxtImg
            :src="news.image"
            sizes="xs:100vw sm:50vw lg:400px"
            format="webp"
            densities="x1"
            alt="News Image"
            class="w-full h-48 object-cover transition-all duration-300 ease-in-out hover:scale-110"
          />
          <div class="flex flex-col py-6 px-4 flex-1">
            <p class="text-xl lg:text-2xl font-semibold mb-2 text-gray-800">
              {{ news.title }}
            </p>
            <div
              class="text-lg lg:text-xl font-normal text-gray-600 mb-4 mt-auto"
            >
              <span
                >{{ news.description.substring(0, 100) }}
                <NuxtLink
                  :to="`/news/${news.id}`"
                  class="text-gray-800 font-semibold"
                >
                  Read More
                </NuxtLink>
                ...
              </span>
            </div>
          </div>
        </div>
      </div>

      <p v-else class="text-xl text-center text-red-500">
        Oops, something went wrong. Please try again later.
      </p>
      <div
        v-if="!loading"
        class="flex justify-center items-center mt-6 space-x-4"
      >
        <button
          @click="currentPage--"
          :disabled="currentPage === 1"
          class="px-4 py-2 bg-gray-300 rounded-lg hover:bg-gray-400 disabled:bg-gray-200"
        >
          Previous
        </button>
        <span
          >Page {{ currentPage }} of
          {{ Math.ceil(data.length / itemsPerPage) }}</span
        >
        <button
          @click="currentPage++"
          :disabled="
            currentPage === Math.ceil(data.length / itemsPerPage)
          "
          class="px-4 py-2 bg-gray-300 rounded-lg hover:bg-gray-400 disabled:bg-gray-200"
        >
          Next
        </button>
      </div>
    </section>
  </main>
</template>

<style scoped>
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
