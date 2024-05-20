<template>
  <div class="book-details-upper">
    <div class="cover-container">
      <img :src="book.thumbnailUrl" :alt="book.title">
    </div>
    <h2 class="book-title">{{ book.title }}</h2>
    <h3 v-for="(author, index) in book.authors" :key="book.id + author" class="book-authors">
      <p>{{ book.authors.length > 1 ? index ===
        book.authors.length - 1 ? `and ${author}` : `${author},` : `${author}` }}</p>
    </h3>
    <p class="book-price">${{ book.price }}</p>
  </div>
  <button @click="$emit('add-to-cart')">Add to cart</button>
</template>

<script setup>
defineEmits(['add-to-cart'])

const props = defineProps({
  book: Object
});

</script>

<style scoped>
.cover-container img {
  width: 80%;
  border: 0.5rem solid #e1e1e3;
  border-radius: 2%;
}

.cover-container img:hover {
  transform: scale(1.1);
  transition: all 0.2s ease-in-out;
}

.book-title {
  line-height: 1.25;
  margin: 0.6rem 0;
  color: rgb(44, 41, 59);
  font-weight: 600;
}

.book-price {
  color: rgb(44, 41, 59);
  font-weight: 500;
}

.book-authors p{
  line-height: 1;
  margin: 0.6rem 0;
}

.book-details button {
  all: unset;
  text-align: center;
  padding: 4px 8px;
  border-radius: 9999px;
  cursor: pointer;
  color: #fff;
  background-color: #de2454;
}

.book-details button:hover {
  transform: scale(1.05);
  background-color: #b41b43;
  transition: all 0.1s ease-in-out;
}
</style>