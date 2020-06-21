<template>
  <div>
    {{ feedback }}
  </div>
</template>

<script>
export default {
  props: {
    lastGuess: {
      type: Number,
      default: NaN
    },
    adjective: {
      type: String,
      default: "silly"
    }
  },
  computed: {
    feedback() {
      let text = "";
      if (this.adjective === "correct") {
        text = `Congratulations, ${this.lastGuess} is exactly right!`;
      } else if (!isNaN(this.lastGuess)) {
        text = `Sorry, ${this.lastGuess} is too ${this.adjective}.`;
      }
      return text;
    }
  }
};
</script>
