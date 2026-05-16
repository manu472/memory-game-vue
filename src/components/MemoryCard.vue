<template>
  <div class="card" @click="$emit('click')">
    <span v-if="card.flipped || card.matched">
      {{ card.value }}
    </span>
    <span v-else>
      ?
    </span>
  </div>
</template>

<script setup>
defineProps({
  card: Object
})
</script>