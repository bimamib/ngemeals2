<template>
  <div class="flex flex-col p-8 pb-0 text-red-600">
    <h1 class="mb-4 text-4xl font-bold">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    await new Promise((resolve) => setTimeout(resolve, 1000)); // Tunggu 1 detik
    try {
      const response = await axiosClient.get(`random.php`);
      meals.value.push(response.data.meals[0]);
    } catch (error) {
      console.error(`Error fetching meal ${i + 1}:`, error.message);
    }
  }
});
</script>
