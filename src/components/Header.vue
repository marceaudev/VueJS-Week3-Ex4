<script setup>
import bookList from '../assets/data.json'

const emit = defineEmits(['changeBookDisplay'])
</script>

<template>
  <header class="container">
    <button v-for="book in bookList" :key="book.id" @click="$emit('changeBookDisplay', book)">
      {{ book.title }}
      <span>({{ book.category }})</span>
    </button>
  </header>
</template>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  height: 100px;
}

button {
  background-color: transparent;
  border: 2px solid orange;
  color: orange;
  border-radius: 5px;
  padding: 10px 15px;
  font-weight: bold;
  font-size: 16px;
}

span {
  color: black;
  font-weight: normal;
  font-size: 12px;
}
</style>
