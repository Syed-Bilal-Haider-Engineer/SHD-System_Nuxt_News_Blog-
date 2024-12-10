    <script setup>
  import { reactive } from "vue";
  
  const form = reactive({
    name: "",
    email: "",
    message: "",
  });
  
  const errors = reactive({});
  
  const onSubmit = () => {
    Object.keys(errors).forEach(key => (errors[key] = ""));
  
    let isValid = true;
  
    if (!form.name) {
      errors.name = "Name is required";
      isValid = false;
    }
  
    if (!form.email) {
      errors.email = "Email is required";
      isValid = false;
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
      errors.email = "Invalid email format";
      isValid = false;
    }
  
    if (!form.message) {
      errors.message = "Message is required";
      isValid = false;
    } else if (form.message.length < 10) {
      errors.message = "Message must be at least 10 characters";
      isValid = false;
    }
  
    if (isValid) {
      alert("Form submitted successfully!");
    }
  };
  </script>

<template>
    <div class="min-h-screen flex items-center justify-center bg-gray-100 py-12 px-6">
      <div class="w-full max-w-lg bg-white shadow-md rounded px-8 py-12">
        <h2 class="text-2xl font-bold text-gray-800 mb-6 text-center">Contact Us</h2>
  
        <form @submit.prevent="onSubmit" novalidate>
          <div class="mb-4">
            <label for="name" class="block text-gray-700 font-medium mb-2">Name</label>
            <input
              type="text"
              id="name"
              v-model="form.name"
              class="w-full border-gray-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            />
            <p v-if="errors.name" class="text-red-500 text-sm mt-2">{{ errors.name }}</p>
          </div>
  
          <div class="mb-4">
            <label for="email" class="block text-gray-700 font-medium mb-2">Email</label>
            <input
              type="email"
              id="email"
              v-model="form.email"
              class="w-full border-gray-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            />
            <p v-if="errors.email" class="text-red-500 text-sm mt-2">{{ errors.email }}</p>
          </div>
  
          <div class="mb-4">
            <label for="message" class="block text-gray-700 font-medium mb-2">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              rows="4"
              class="w-full border-gray-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
            ></textarea>
            <p v-if="errors.message" class="text-red-500 text-sm mt-2">{{ errors.message }}</p>
          </div>
  
          <button
            type="submit"
            class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 transition"
          >
            Submit
          </button>
        </form>
      </div>
    </div>
  </template>
  
  <style scoped>
  body {
    font-family: 'Inter', sans-serif;
  }
  </style>
  