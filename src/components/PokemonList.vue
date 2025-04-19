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
    <div class="card cardListPokemon text-center">
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

<style scoped>
.cardListPokemon {
  background: #4f3ffb;
  background: radial-gradient(
    circle,
    rgba(79, 63, 251, 1) 0%,
    rgba(70, 252, 249, 0.54) 100%
  );
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}

.cardListPokemon:hover {
  background: #4f3ffb;
  transform: scale(1.05);
  transition: all 0.3s ease-in-out;
  background: #fb3f6b;
  background: radial-gradient(
    circle,
    rgba(251, 63, 107, 0.08) 0%,
    rgba(70, 252, 249, 0.54) 100%
  );
}

.cardListPokemon img:hover {
  padding: 0.2rem;
}
</style>
