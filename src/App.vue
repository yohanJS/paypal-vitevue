<script setup>
import HelloWorld from './components/HelloWorld.vue';
import NavBar from './components/NavBar.vue';
import PayPalButtons from './components/PayPalButtons.vue';
import Footer from './components/Footer.vue';
</script>

<template>
  <div class="bg-white">
    <h3>Checkout</h3>
  </div>
  <NavBar></NavBar>
  <PayPalButtons></PayPalButtons>
  <Footer></Footer>
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
