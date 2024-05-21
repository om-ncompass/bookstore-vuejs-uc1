<template>
  <header>
    <div class="logo">
      <img :src="logo" alt="bookstore-logo">
    </div>
    <div class="cart-container" @click="$emit('cart-open')">
      <div><img src="https://rails-assets-us.bookshop.org/ds/images/basket.76e8fe7b84404cf9232df8188db62fd33e0c6453.svg"
          alt="cart"></div>
      <div class="cart-items-quanitity"><span>&lpar;{{ cartQuanitity }}&rpar;</span></div>
    </div>
  </header>
</template>

<script setup>
import logo from '../assets/logo.png'

defineEmits(['cart-open'])

const props = defineProps({
  cartQuanitity: Number
})
</script>

<style>
header {
  padding: 0 1rem;
}

.cart-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  cursor: pointer;
  padding: 4px;
}

.cart-container:hover {
  background-color: #eae9ed;
  border-radius: 10px;
  transform: scale(1.05);
  transition: all 0.1s ease-in-out;
}

.cart-container img {
  width: 130%;
}

.cart-items-quanitity {
  font-size: 20px;
}

header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #eae9ed;
}
</style>