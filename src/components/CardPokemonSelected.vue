<script setup>
import { defineProps } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  BASE_URL: {
    type: String,
    required: true,
  },
  xp: {
    type: String,
    required: true,
  },
  height: {
    type: String,
    required: true,
  },
});

console.log(props.BASE_URL);
console.log("Esse daqui e o name: " + props.name);
</script>

<template>
  <div class="card">
    <img
      :src="props.BASE_URL"
      height="300"
      class="card-img-top pt-4"
      :alt="props.name"
    />
    <div class="card-body text-center">
      <h5 class="card-title">{{ props.name }}</h5>
      <hr />
      <div class="row">
        <section class="col">
          <strong>XP: </strong>
          <span>{{ props.xp }}</span>
        </section>
        <section class="col">
          <strong>Altura: </strong>
          <span>{{ props.height }}</span>
        </section>
      </div>
    </div>
  </div>
</template>
