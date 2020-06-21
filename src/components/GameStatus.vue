<template>
  <div :class="computedClass">
    {{ status }}
  </div>
</template>

<script>
export default {
  props: {
    gameStarted: Boolean,
    gameOver: Boolean,
    gameWon: Boolean
  },
  computed: {
    status() {
      let text = "";
      if (this.gameOver) {
        text = this.gameWon
          ? "You win!"
          : "That was your last guess. You lose.";
      } else if (this.gameStarted) {
        text = "Guess again.";
      }
      return text;
    },
    computedClass() {
      return this.gameOver ? "game-over" : "default";
    }
  }
};
</script>

<style scoped>
.game-over {
  font-weight: bold;
}
</style>
