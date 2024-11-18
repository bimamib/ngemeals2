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
  try {
    const requests = Array.from({ length: 10 }).map(() =>
      axiosClient.get(`random.php`)
    );
    const responses = await Promise.all(requests);
    meals.value = responses.map(({ data }) => data.meals[0]);
  } catch (error) {
    console.error("Error fetching meals:", error.message);
  }
});
</script>
