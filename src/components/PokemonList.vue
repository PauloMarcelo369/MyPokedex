<script setup>
import { onMounted, defineProps, ref } from "vue";
import api from "../api";

const pokemonName = ref("");
const pokemonData = ref({});

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  BASE_IMAGE_URL: {
    type: String,
    required: true,
  },
});

onMounted(async () => {
  pokemonName.value = props.name;
  console.log(props.BASE_IMAGE_URL);
  try {
    const response = await api.get(`pokemon/${pokemonName.value}`);
    pokemonData.value = response.data;
  } catch (err) {
    console.log(err);
  }
});
</script>

<template>
  <div class="col-4 p-2 mb-4">
    <div class="card">
      <p class="text-center">{{ pokemonName }}</p>
      <img
        :src="props.BASE_IMAGE_URL"
        :alt="pokemonName"
        class="card-image-top"
        height="100"
      />
    </div>
  </div>
</template>
