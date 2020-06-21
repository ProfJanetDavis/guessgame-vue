<template>
  <form id="app" @submit.prevent="onPlayAgain">
    <h1>The Lo-Hi Game</h1>
    <guess-input
      :disabled="gameOver"
      :max-guess="maxTarget"
      @new-guess="onNewGuess"
    ></guess-input>
    <guess-history
      :last-guess="lastGuess"
      :last-guess-feedback="feedback"
      :gameOver="gameOver"
    ></guess-history>
    <guess-feedback
      :last-guess="lastGuess"
      :adjective="feedback"
    ></guess-feedback>
    <game-status
      :gameStarted="gameStarted"
      :gameOver="gameOver"
      :gameWon="gameWon"
    ></game-status>
    <input type="submit" value="Play again!" v-if="gameOver" />
  </form>
</template>

<script>
import GuessInput from "./components/GuessInput.vue";
import GuessHistory from "./components/GuessHistory.vue";
import GuessFeedback from "./components/GuessFeedback.vue";
import GameStatus from "./components/GameStatus.vue";

const maxValue = 100;
function chooseTarget() {
  return Math.floor(Math.random() * maxValue) + 1;
}

export default {
  name: "App",
  components: {
    GuessInput,
    GuessHistory,
    GuessFeedback,
    GameStatus
  },
  data() {
    return {
      maxTarget: maxValue,
      maxGuesses: 8,
      guessCount: 0,
      target: chooseTarget(),
      lastGuess: NaN,
      feedback: "",
      gameOver: false,
      gameWon: false
    };
  },
  computed: {
    gameStarted() {
      console.log(!isNaN(this.lastGuess));
      return !isNaN(this.lastGuess);
    }
  },
  methods: {
    onNewGuess(newGuess) {
      this.lastGuess = newGuess;
      this.guessCount += 1;
      if (newGuess === this.target) {
        this.feedback = "correct";
        this.gameWon = true;
        this.gameOver = true;
      } else {
        this.feedback = newGuess > this.target ? "high" : "low";
        this.gameOver = this.guessCount === this.maxGuesses;
      }
    },
    onPlayAgain() {
      this.guessCount = 0;
      this.target = chooseTarget();
      this.lastGuess = NaN;
      this.feedback = "";
      this.gameWon = false;
      this.gameOver = false;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 60px;
  background: "coral";
}

div {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>
