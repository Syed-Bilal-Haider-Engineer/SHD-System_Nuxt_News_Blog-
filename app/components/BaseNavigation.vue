<script setup lang="ts"></script>

<template>
  <header class="py-4 border-b">
    <nav class="flex container items-center">
      <a href="" class="flex gap-1 items-center">
        <img class="w-14" src="/icon-green.png" alt="" />
        <span class="text-3xl font-bold">News Blog</span>
      </a>
      <ul class="flex gap-6 ml-auto text-xl font-bold capitalize">
        <NuxtLink to="/"
        class="text-gray-800 font-semibold">
          Home
        </NuxtLink>
        <li>
          <NuxtLink
            to="/contact"
            class="text-gray-800 font-semibold"
            >
              contact us
          </NuxtLink>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style scoped></style>
