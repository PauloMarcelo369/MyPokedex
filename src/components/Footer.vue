<script setup></script>

<template>
  <footer class="bg-danger text-white text-center py-3">
    <p>&copy; {{ new Date().getFullYear() }} Pokedex. All rights reserved.</p>
    <p>Made with ❤️ by Paulo Marcelo</p>
  </footer>
</template>

<style scoped>
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 90px;
  left: 0;
  z-index: 1;
}
</style>
