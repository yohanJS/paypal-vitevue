<script setup>
import NavBar from './components/NavBar.vue';
import PayPalButtons from './components/PayPalButtons.vue';
</script>

<template>
  <div class="bg-white">
    <img src="/vite.svg" class="logo" alt="Vite logo" />
    <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    <h3>PayPal SDK Integration</h3>
  </div>
  <NavBar></NavBar>
  <PayPalButtons></PayPalButtons>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
