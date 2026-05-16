<template>
  <div class="modal">
    <div class="content">
      <h2>¡Has ganado!</h2>

      <p>Puntuación: {{ score }}</p>
      <p>Movimientos: {{ moves }}</p>
      <p>Tiempo: {{ time }} segundos</p>

      <button @click="$emit('restart')">
        Jugar otra vez
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  score: Number,
  moves: Number,
  time: Number
})
</script>