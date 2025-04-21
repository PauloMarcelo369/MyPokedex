<script setup>
import { RouterView } from "vue-router";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <Header></Header>
  <div class="main">
    <router-view></router-view>
  </div>

  <Footer></Footer>
</template>

<style>
body {
  height: 100vh;
  background: #070769;
  background: linear-gradient(
    90deg,
    rgba(7, 7, 105, 1) 0%,
    rgba(10, 10, 196, 1) 15%,
    rgba(189, 32, 92, 1) 100%
  );
}
</style>
