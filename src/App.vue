<script setup>
import Header from './components/Header.vue'
import Book from './components/Book.vue'
import Article from './components/Article.vue'
import { ref, computed } from 'vue'

const selectedBookIndex = ref({})

const changeBookIndex = (index) => {
  selectedBookIndex.value = index
}

const reset = () => {
  selectedBookIndex.value = {}
}

const rateAverage = computed(() => {
  let total = 0

  for (let i = 0; i < selectedBookIndex.value.rates.length; i++) {
    total += selectedBookIndex.value.rates[i]
  }
  const numOfrates = selectedBookIndex.value.rates.length

  return total / numOfrates
})
</script>

<template>
  <Header @changeBookDisplay="changeBookIndex" />

  <main class="container">
    <Book
      v-if="selectedBookIndex.category === 'livre'"
      :book="selectedBookIndex"
      :rateAverage="rateAverage"
    />
    <Article
      v-else-if="selectedBookIndex.category === 'article'"
      :article="selectedBookIndex"
      :rateAverage="rateAverage"
    />
    <div v-else>
      <h1>Faites votre choix</h1>
    </div>
    <div>
      <button @click="reset">Reset</button>
    </div>
  </main>
</template>

<style scoped>
main {
  height: calc(100vh - 101px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}

main > div {
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  position: absolute;
  bottom: 50px;
  right: 0;
  background-color: orange;
  border: none;
  color: white;
  padding: 10px;
  border-radius: 10px;
}

h1 {
  font-size: 34px;
  font-weight: bold;
  filter: drop-shadow(0px 0px 2px orange);
}
</style>
