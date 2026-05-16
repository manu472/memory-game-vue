<template>
  <div class="app">
    <h1>Juego de memoria 🧠</h1>

    <div class="board">
      <div
        v-for="(card, index) in cards"
        :key="index"
        class="card"
        :class="{ flipped: card.flipped || card.matched }"
        @click="flipCard(card)"
      >
        <div class="front">❓</div>
        <div class="back">{{ card.value }}</div>
      </div>
    </div>

    <button @click="resetGame">Reiniciar 🔄</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      values: ["🍎", "🍌", "🍇", "🍉", "🍒", "🍍", "🥝", "🍑"],
      cards: [],
      firstCard: null,
      secondCard: null,
      lock: false,
    };
  },

  mounted() {
    this.resetGame();
  },

  methods: {
    shuffle(array) {
      return array.sort(() => Math.random() - 0.5);
    },

    resetGame() {
      const duplicated = [...this.values, ...this.values];

      this.cards = this.shuffle(duplicated).map((value) => ({
        value,
        flipped: false,
        matched: false,
      }));

      this.firstCard = null;
      this.secondCard = null;
      this.lock = false;
    },

    flipCard(card) {
      if (this.lock || card.flipped || card.matched) return;

      card.flipped = true;

      if (!this.firstCard) {
        this.firstCard = card;
        return;
      }

      this.secondCard = card;
      this.lock = true;

      this.checkMatch();
    },

    checkMatch() {
      if (this.firstCard.value === this.secondCard.value) {
        this.firstCard.matched = true;
        this.secondCard.matched = true;
        this.resetTurn();
      } else {
        setTimeout(() => {
          this.firstCard.flipped = false;
          this.secondCard.flipped = false;
          this.resetTurn();
        }, 800);
      }
    },

    resetTurn() {
      this.firstCard = null;
      this.secondCard = null;
      this.lock = false;
    },
  },
};
</script>

<style>
.app {
  text-align: center;
  font-family: Arial, sans-serif;
}

.board {
  display: grid;
  grid-template-columns: repeat(4, 80px);
  gap: 10px;
  justify-content: center;
  margin: 20px 0;
}

.card {
  width: 80px;
  height: 80px;
  cursor: pointer;
  position: relative;
  perspective: 1000px;
}

.card .front,
.card .back {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  border-radius: 8px;
  transition: transform 0.3s;
}

.card .front {
  background: #333;
  color: white;
}

.card .back {
  background: white;
  transform: rotateY(180deg);
}

.card.flipped .front {
  transform: rotateY(180deg);
}

.card.flipped .back {
  transform: rotateY(0);
}
</style>