<template>
  <main>
    <Header :cartQuanitity="cartQuanitity"/>
    <Home @add-to-cart="handleAddToCart" />
  </main>
</template>

<script setup>
import Home from './components/Home.vue';
import Header from './components/Header.vue'
import { ref } from 'vue';

const cartQuanitity = ref(0);

function handleAddToCart() {
  cartQuanitity.value += 1;
}
</script>
<style scoped>
main {
  padding: 1rem;
}
</style>