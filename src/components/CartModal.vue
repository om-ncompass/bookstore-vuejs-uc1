<template>
  <div class="cart-modal-backdrop" style="opacity: 1;">
    <div class="cart-modal" v-if="cartItems.length">
      <div class="cart-items">
        <div class="cart-item cart-items-column">
          <p>Item</p>
          <p>Price</p>
        </div>
        <div class="cart-items" v-for="cartItem in cartItems" :key="cartItem.id">
          <div v-if="cartItem.quantity" class="cart-item">
            <p>{{ cartItem.title }} X {{ cartItem.quantity }}
              <span>
                <button class="add-item" @click="$emit('add-item', cartItem.id)">+</button>
                <button class="remove-item" @click="$emit('remove-item', cartItem.id)">-</button>
              </span>
            </p>
            <p>&#8377;{{ cartItem.price * cartItem.quantity }}</p>
          </div>
        </div>
      </div>
      <div class="total-price-container">
        <p>Total price : </p>
        <p>&#8377;{{ totalPrice }}</p>
      </div>
      <div class="buttons-container">
        <button @click="$emit('cart-close')">Close Cart</button>
        <button @click="$emit('checkout-open', totalPrice)">Checkout</button>
      </div>
    </div>
    <div class="empty-cart" v-else>
      <h2>Cart is empty.</h2>
      <div class="buttons-container">
        <button @click="$emit('cart-close')">Close Cart</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue"

const totalPrice = computed(() => {
  return props.cartItems.reduce((accumulator, cartItem) => accumulator + cartItem.quantity * cartItem.price, 0)
})

defineEmits(['cart-close', 'checkout-open', 'add-item', 'remove-item'])

const props = defineProps({
  cartItems: Array
})
</script>

<style scoped>
.cart-modal-backdrop {
  position: fixed;
  top: 30%;
  bottom: 0;
  right: 0;
  left: 40%;
  width: fit-content;
  height: fit-content;
  background: #E9DCC9;
  box-shadow: 2px 2px 20px 1px;
  padding: 1rem 2rem;
  border-radius: 4px;
  pointer-events: all;
}

.cart-items-column {
  margin-bottom: 0.8rem;
}

.cart-items-column>p {
  font-weight: 500;
  text-decoration: underline;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  margin: 0.6rem 0;
}

.cart-item button {
  text-align: center;
  margin: 0 0.2rem;
  border-radius: 9999px;
  border: none;
  color: #fff;
  cursor: pointer;
}

.add-item {
  font-size: medium !important;
  background-color: green !important;
}

.remove-item {
  font-size: medium !important;
  background-color: red !important;
}

.total-price-container {
  display: flex;
  justify-content: space-between;
  margin: 0.5rem 0;
}

.total-price-container p {
  font-weight: 600;
}

.buttons-container {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  margin-top: 1rem;
}

.buttons-container>button {
  all: unset;
  text-align: center;
  padding: 2px 4px;
  border-radius: 8px;
  cursor: pointer;
  color: #fff;
  background-color: #de2454;
  cursor: pointer;
}

.buttons-container>button:hover,
.cart-item button:hover {
  transform: scale(1.05);
  background-color: #b41b43;
  transition: all 0.1s ease-in-out;
}

.empty-cart {
  text-align: center;
}
</style>