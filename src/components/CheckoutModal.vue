<template>
  <div class="cart-modal-backdrop">
    <div v-if="!isSubmitted">
      <div class="price-info">
        <p>Total :</p>
        <p>&#8377;{{ totalPrice }}</p>
      </div>
      <form class="form-container">
        <div class="form-control">
          <input type="text" name="name" placeholder="Your full name" required>
        </div>
        <div class="form-control">
          <input type="email" name="email" placeholder="Your email" required>
        </div>
        <div class="form-control">
          <input type="tel" name="phone-number" placeholder="Your phone number" required>
        </div>
        <div class="form-control">
          <input type="text" name="address" placeholder="Your address" required>
        </div>
        <div class="buttons-container form-control">
          <button type="button" @click="handleCheckoutClose">Close</button>
          <button type="submit" @click="handleSubmit">Submit</button>
        </div>
      </form>
    </div>
    <div class="order-placed" v-else>
      <p>Order placed succesfully.</p>
      <div class="buttons-container">
        <button type="button" @click="$emit('checkout-close')">Close</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['checkout-close', 'form-submit'])

const props = defineProps({
  totalPrice: Number,
  isSubmitted: Boolean
})

function handleSubmit(e) {
  e.preventDefault();
  emit('form-submit')
}

function handleCheckoutClose() {
  emit('checkout-close');
}

</script>

<style scoped>
.cart-modal-backdrop {
  position: fixed;
  top: 30%;
  bottom: 0;
  right: 0;
  left: 40%;
  width: 20%;
  height: 50%;
  background: #E9DCC9;
  box-shadow: 2px 2px 20px 1px;
  padding: 1rem 2rem;
  border-radius: 4px;
  pointer-events: all;
}

.price-info {
  display: flex;
  gap: 1rem;
}

.price-info>p {
  font-weight: 500;
  font-size: large;
}

.form-container {
  margin: 1rem 0;
}

.form-control {
  margin: 1rem 0;
}

input {
  all: unset;
  border-bottom: 1px solid #de2454;
}

.buttons-container {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
}

button {
  all: unset;
  text-align: center;
  padding: 4px;
  border-radius: 8px;
  cursor: pointer;
  color: #fff;
  background-color: #de2454;
  cursor: pointer;
  margin-top: 12px;
  transition: transform 0.1s ease-in-out;
}

button:hover {
  transform: scale(1.05);
  background-color: #b41b43;
}

.order-placed {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>