<template>
  <!-- Detail Meals -->
  <Loading :visible="loading" />
  <div v-if="!loading" class="max-w-[800px] mx-auto p-10">
    <h1 class="mb-5 text-4xl font-bold">{{ meal.strMeal }}</h1>
    <div class="px-4 py-4 bg-white shadow rounded-xl">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="max-w-[100%] rounded-lg"
      />
    </div>
    <div
      class="grid grid-cols-1 px-2 py-2 text-lg sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-3"
    >
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div><strong class="font-bold">Area:</strong> {{ meal.strArea }}</div>
      <div><strong class="font-bold">Tags:</strong> {{ meal.strTags }}</div>
    </div>

    <div class="my-3 text-justify">
      {{ meal.strInstructions }}
    </div>

    <!-- Ingredients and Measures -->
    <div class="grid grid-cols-1 sm:grid-cols-2">
      <!-- Ingredients -->
      <div>
        <h2 class="mb-2 text-2xl font-semibold">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <!-- Measures -->
      <div>
        <h2 class="mb-2 text-2xl font-semibold">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>

      <div class="mt-4">
        <YouTubeButton :href="meal.strYoutube" />
        <a
          :href="meal.strSource"
          target="_blank"
          class="inline-flex items-center px-3 py-2 ml-3 text-sm font-medium text-yellow-500 transition-colors hover:text-yellow-800 disabled:opacity-50 disabled:pointer-events-none"
        >
          View Original
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";
import Loading from "../components/Loading.vue";

const route = useRoute();
const meal = ref({});
const loading = ref(true);

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
    loading.value = false;
  });
});
</script>
