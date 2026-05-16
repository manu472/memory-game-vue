<template>
  <div class="board">
    <MemoryCard
      v-for="card in cards"
      :key="card.id"
      :card="card"
      @click="$emit('flip', card)"
    />
  </div>
</template>

<script setup>
import MemoryCard from './MemoryCard.vue'

defineProps({
  cards: Array
})
</script>