<template>
  <main :class="{ 'cart-open': isCartOpen || isCheckoutOpen }">
    <CartModal :cartItems="cart" v-show="isCartOpen" @cart-close="handleCartClose" @checkout-open="handleCheckoutOpen"
      @add-item="handleAddItem" @remove-item="handleRemoveItem" />
    <CheckoutModal v-show="isCheckoutOpen" :totalPrice="totalPrice" @checkout-close="handleCheckoutClose" />
    <Header :cartQuanitity="cartQuanitity" @cart-open="handleCartOpen" />
    <Home @add-to-cart="handleAddToCart" />
  </main>
</template>

<script setup>
import Home from './components/Home.vue';
import Header from './components/Header.vue'
import CartModal from './components/CartModal.vue'
import CheckoutModal from './components/CheckoutModal.vue';
import { computed, ref } from 'vue';

const cart = ref([]);
const isCartOpen = ref(false);
const isCheckoutOpen = ref(false);
const totalPrice = ref(0);

const cartQuanitity = computed(() => {
  return cart.value.reduce((accumulator, cartItem) => accumulator + cartItem.quantity, 0);
})

function handleAddToCart(bookData) {
  const bookIndexInCart = cart.value.findIndex(item => item.id === bookData.id);

  if (bookIndexInCart === -1) {
    cart.value.push(bookData)
  } else {
    cart.value[bookIndexInCart].quantity += 1;
  }
}

function handleCartOpen() {
  isCartOpen.value = true;
}

function handleCartClose() {
  isCartOpen.value = false;
}

function handleCheckoutOpen(_totalPrice) {
  totalPrice.value = _totalPrice;
  isCheckoutOpen.value = true;
  isCartOpen.value = false;
}

function handleCheckoutClose() {
  isCheckoutOpen.value = false;
}

function handleAddItem(bookId) {
  const bookIndexInCart = cart.value.findIndex(item => item.id === bookId);
  cart.value[bookIndexInCart].quantity += 1;
}

function handleRemoveItem(bookId) {
  const bookIndexInCart = cart.value.findIndex(item => item.id === bookId);
  cart.value[bookIndexInCart].quantity -= 1;
}
</script>

<style scoped>
main {
  padding: 1rem;
}

.cart-open {
  opacity: 0.8;
  pointer-events: none;
}
</style>