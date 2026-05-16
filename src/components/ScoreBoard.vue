<template>
  <div class="scoreboard">
    <p>Movimientos: {{ moves }}</p>
    <p>Puntos: {{ score }}</p>
    <p>Tiempo: {{ time }} s</p>

    <button @click="$emit('restart')">
      Reiniciar
    </button>
  </div>
</template>

<script setup>
defineProps({
  moves: Number,
  score: Number,
  time: Number
})
</script>