<script setup>
import api from "../api";
import { ref, onMounted, watch, computed } from "vue";
import PokemonList from "../components/PokemonList.vue";
import CardPokemonSelected from "../components/CardPokemonSelected.vue";

const pokemons = ref([]);

const searchPokemonField = ref("");
const loading = ref(false);
const name = ref("");
const error = ref(null);
const currentPokemon = ref({});
const BASE_IMAGE_URL =
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/";

const fetchPokemons = async () => {
  try {
    const response = await api.get("pokemon?limit=151&offset=0");
    pokemons.value = response.data.results;
  } catch (err) {
    error.value = err;
    console.log(err);
  }
};

const pokemonEventClick = async (pokemon) => {
  loading.value = true;
  try {
    const response = await api.get(`pokemon/${pokemon.name}`);
    currentPokemon.value = response.data;
    console.log(currentPokemon.value);
  } catch (err) {
    console.log("deu erro");
  } finally {
    loading.value = false;
  }
};

const filteredPokemons = computed(() => {
  if (pokemons.value && searchPokemonField) {
    return pokemons.value.filter((pokemon) =>
      pokemon.name
        .toLowerCase()
        .includes(searchPokemonField.value.toLowerCase())
    );
  }
  return pokemons.value;
});

onMounted(() => {
  fetchPokemons();
});
</script>

<template>
  <main>
    <div class="container text-center">
      <div class="container">
        <div class="row mt-4">
          <div class="col-sm-12 col-md-6">
            <div v-if="loading" class="">carregando</div>
            <CardPokemonSelected
              v-else
              :name="currentPokemon?.name"
              :BASE_URL="
                currentPokemon?.sprites?.other.dream_world.front_default
              "
              :xp="currentPokemon?.base_experience"
              :height="currentPokemon?.height"
              v-show="!loading"
            />
          </div>
          <div class="col-sm-12 col-md-6">
            <div class="card p-2 card-list">
              <div class="mb-3">
                <label for="exampleFormControlInput" class="form-label"
                  >Pesquisar</label
                >
                <input
                  type="text"
                  class="form-control"
                  id="exampleFormControlInput"
                  placeholder="Pokemon name"
                  v-model="searchPokemonField"
                />
              </div>
              <div class="card-body row g-2">
                <PokemonList
                  v-for="pokemon in filteredPokemons"
                  :key="pokemon.name"
                  :name="pokemon.name"
                  :BASE_IMAGE_URL="
                    BASE_IMAGE_URL + pokemon.url.split('/')[6] + '.svg'
                  "
                  @click="pokemonEventClick(pokemon)"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.card-list {
  height: 75vh;
  overflow-y: scroll;
  overflow-x: hidden;
}
</style>
