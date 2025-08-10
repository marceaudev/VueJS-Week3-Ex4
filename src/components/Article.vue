<script setup>
import { computed } from 'vue'

const props = defineProps({
  article: {
    type: Object,
    required: true,
  },
  rateAverage: {
    type: Number,
    required: true,
  },
})

const contentParagraphs = computed(() => {
  const lines = props.article.content.split('\n')
  const result = []
  for (let i = 0; i < lines.length; i++) {
    result.push(lines[i])
  }
  return result
})
</script>

<template>
  <section>
    <h2>{{ article.title }}</h2>
    <p v-for="(paragraph, index) in contentParagraphs" :key="index">
      {{ paragraph }}
    </p>
    <span v-if="article.author && article.author.name" class="author">
      {{ article.author.name }}
    </span>
    <span v-else-if="article.author" class="author">
      {{ article.author }}
    </span>
    <div class="like">
      <font-awesome-icon v-if="article.rates.length > 0" :icon="['fas', 'thumbs-up']" />
      <span :class="{ unliked: article.rates.length === 0 }">
        {{ article.rates.length > 0 ? rateAverage : 'Pas encore de like' }}
      </span>
    </div>
  </section>
</template>
