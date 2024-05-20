<template>
  <header>
    <div class="logo">
      <img :src="logo" alt="bookstore-logo">
    </div>
    <div class="cart-container">
      <div><img src="https://rails-assets-us.bookshop.org/ds/images/basket.76e8fe7b84404cf9232df8188db62fd33e0c6453.svg"
          alt="cart"></div>
      <div class="cart-items-quanitity"><span>&lpar;{{ 0 }}&rpar;</span></div>
    </div>
  </header>
</template>

<script setup>
import logo from '../assets/logo.png'
</script>

<style>
.cart-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
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