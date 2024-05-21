<template>
  <div class="booklist-container">
    <div v-if="books.length" class="booklist">
      <div v-for="book in books" :key="book.id" class="book-details">
        <Book :book="book" @add-to-cart="(bookData) => $emit('add-to-cart', bookData)" />
      </div>
    </div>
    <div v-else class="no-books">
      <h2>No books to display</h2>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Book from './Book.vue';

const books = ref([])

defineEmits(['add-to-cart'])

onMounted(async () => {
  const response = await fetch('http://localhost:5000/books')
  const data = await response.json()
  books.value = data;
})
</script>

<style scoped>
.booklist-container {
  padding: 4rem 2rem;
}

.booklist {
  display: grid;
  grid-column-gap: 1.5rem;
  -moz-column-gap: 1.5rem;
  column-gap: 1.5rem;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  grid-row-gap: 2rem;
  row-gap: 2rem;
}

.book-details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 0.6rem;
}

.no-books {
  text-align: center;
}
</style>