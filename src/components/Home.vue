<template>
  <div class="booklist-container">
    <div v-if="books.length" class="booklist">
      <div v-for="book in books" :key="book.id" class="book-details">
        <div class="book-details-upper">
          <div class="cover-container">
            <img :src="book.thumbnailUrl" :alt="book.title">
          </div>
          <h2 class="book-title">{{ book.title }}</h2>
          <h3 v-for="(author, index) in book.authors" :key="book.id + author" class="book-authors"><p>{{ book.authors.length > 1 ? index ===
            book.authors.length - 1 ? `and ${author}` : `${author},` : `${author}`}}</p></h3>
          <p>${{ book.price }}</p>
        </div>
        <button>Add to cart</button>
      </div>
    </div>
    <div v-else>
      <h2>No books to display</h2>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const books = ref([])

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

.book-details img {
  width: 80%;
  border: 0.5rem solid #e1e1e3;
  border-radius: 2%;
}

.book-details img:hover {
  transform: scale(1.1);
  transition: all 0.2s ease-in-out;
}

.book-title {
  line-height: 1.25;
  margin: 0.6rem 0;
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