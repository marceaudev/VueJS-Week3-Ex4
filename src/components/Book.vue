<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  book: {
    type: Object,
    required: true,
  },
  rateAverage: {
    type: Number,
    required: true,
  },
})

const synopsisParagraphs = computed(() => {
  const lines = props.book.synopsis.split('\n')
  const result = []
  for (let i = 0; i < lines.length; i++) {
    result.push(lines[i])
  }
  return result
})

const isRolled = ref(true)
</script>

<template>
  <section>
    <span v-if="book.numberOfPage && book.numberOfPage < 250" class="info-book">Petit livre</span>
    <h2>{{ book.title }}</h2>
    <div :class="{ roll: isRolled }">
      <p v-for="(paragraph, index) in synopsisParagraphs" :key="index">
        {{ paragraph }}
      </p>
    </div>
    <div>
      <font-awesome-icon
        class="roller"
        v-if="isRolled"
        :icon="['fas', 'chevron-down']"
        @click="isRolled = false"
      />
      <font-awesome-icon
        class="roller"
        v-else="!isRolled"
        :icon="['fas', 'chevron-up']"
        @click="isRolled = true"
      />
    </div>
    <span v-if="book.author && book.author.name" class="author">
      {{ book.author.name }}
    </span>
    <span v-else-if="book.author" class="author">
      {{ book.author }}
    </span>
    <div class="like">
      <font-awesome-icon v-if="book.rates.length > 0" :icon="['fas', 'thumbs-up']" />
      <span :class="{ unliked: book.rates.length === 0 }">
        {{ book.rates.length > 0 ? rateAverage : 'Pas encore de like' }}
      </span>
    </div>
  </section>
</template>

<style scoped>
.info-book {
  position: absolute;
  right: -20px;
  top: -20px;
  width: 60px;
  height: 60px;
  background: orange;
  display: flex;
  align-items: center;
  text-align: center;
  color: white;
  border-radius: 100%;
}

.roll {
  height: 100px;
  overflow-y: hidden;
}

.roller {
  font-size: 20px;
}

.roller:hover {
  cursor: pointer;
  transform: scale(1.1);
}
</style>
