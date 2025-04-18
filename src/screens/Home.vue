<script setup>
import api from "../api";
import { ref, onMounted } from "vue";
import PokemonList from "../components/PokemonList.vue";

const pokemons = ref([]);
const loading = ref(true);
const error = ref(null);
const page = ref(1);
const limit = ref(20);
const BASE_IMAGE_URL =
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/";
onMounted(async () => {
  try {
    const response = await api.get("pokemon?limit=10&offset=0");
    pokemons.value = response.data.results;
  } catch (err) {
    error.value = err;
    console.log(err);
  }
});
</script>

<template>
  <main>
    <div class="container text-center">
      <div class="container">
        <div class="row mt-4">
          <!-- <div class="col-sm-12 col-md-6">
            <div class="card" style="width: 18rem">
              <img
                src="https://th.bing.com/th/id/R.7482145a4e22bdfca867315c0efa9afd?rik=Nar0DvqIbuihAg&pid=ImgRaw&r=0"
                class="card-img-top"
                alt="..."
              />
              <div class="card-body">
                <h5 class="card-title">Pikachu</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div> -->
          <div class="col-sm-12 col-md-6">
            <div v-show="loading" class="card-body row">
              <span class="visually-hidden">Loading...</span>
            </div>
            <div class="card p-2">
              <div class="card-body row g-2">
                <PokemonList
                  v-for="pokemon in pokemons"
                  :key="pokemon.name"
                  :name="pokemon.name"
                  :BASE_IMAGE_URL="
                    BASE_IMAGE_URL + pokemon.url.split('/')[6] + '.svg'
                  "
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
