<template>
  <div class="p-8 pb-0">
    <h1 class="mb-4 text-4xl font-bold text-red-600">Meals by Letter</h1>
  </div>
  <div class="flex flex-wrap justify-center gap-3 px-8 mb-6">
    <router-link
      :to="{ name: 'byLetter', params: { letter } }"
      v-for="letter of letters"
      :key="letter"
      class="flex items-center justify-center w-2 h-2 transition-all hover:text-red-600 hover:scale-150"
      @click.native="startLoading"
    >
      {{ letter }}
    </router-link>

    <Loading :visible="loading" />
  </div>

  <Meals v-if="!loading" :meals="meals || []" />
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";
import Loading from "../components/Loading.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);
const loading = ref(false);

function startLoading() {
  loading.value = true;
}

async function fetchMealsByLetter(letter) {
  loading.value = true;

  await new Promise((resolve) => setTimeout(resolve, 500));

  await store.dispatch("searchMealsByLetter", letter);

  await new Promise((resolve) => setTimeout(resolve, 500));

  loading.value = false;
}

watch(
  () => route.params.letter,
  (newLetter) => {
    fetchMealsByLetter(newLetter);
  }
);

onMounted(() => {
  fetchMealsByLetter(route.params.letter);
});
</script>
