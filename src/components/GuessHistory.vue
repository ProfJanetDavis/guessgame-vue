<template>
  <div>
    Previous guesses:
    <ul>
      <li v-for="guess in guesses" :key="guess.id">
        <span :class="guess.feedback">{{ guess.value }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import uniqueId from "lodash.uniqueid";

export default {
  props: {
    lastGuess: {
      type: Number,
      required: true
    },
    lastGuessFeedback: {
      type: String,
      required: true
    },
    gameOver: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      guesses: []
    };
  },
  methods: {
    reset() {
      this.guesses = [];
    }
  },
  watch: {
    lastGuess: function(newGuess) {
      this.guesses.push({
        id: uniqueId("guess-"),
        value: newGuess,
        feedback: this.lastGuessFeedback
      });
    },
    gameOver: function(newVal, oldVal) {
      // When gameOver goes from true to false, reset
      if (!newVal && oldVal) {
        this.reset();
      }
    }
  }
};
</script>

<style scoped>
ul {
  display: inline;
  padding-right: 0;
}
li {
  display: inline;
  padding-right: 1ex;
}
span.high {
  color: red;
}
span.low {
  color: blue;
}
span.correct {
  color: lime;
}
</style>
