//TODO: Make magic #s into props
<template>
  <form @submit.prevent="onSubmit">
    <input
      @focus="onFocus"
      type="text"
      id="guess-input"
      name="guess"
      autocomplete="off"
      v-model.lazy.trim="newGuess"
      :disabled="disabled"
    />
    <label for="guess-input" :disabled="disabled">
      Enter a number 1-{{ maxGuess }}:
    </label>
    <input type="submit" value="Guess!" :disabled="disabled" />
    <span id="input-error">{{ error }}</span>
  </form>
</template>

<script>
export default {
  props: {
    maxGuess: {
      type: Number,
      required: true
    },
    disabled: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      newGuess: "",
      error: ""
    };
  },
  methods: {
    onSubmit() {
      let guess = parseInt(this.newGuess);
      if (isNaN(guess)) {
        this.error = `"${this.newGuess}" is not a number.`;
      } else if (guess < 1 || guess > this.maxGuess) {
        this.error = `Your guess should be between 1 and ${this.maxGuess}.`;
      } else {
        this.$emit("new-guess", guess);
      }
      this.newGuess = "";
    },
    onFocus() {
      this.error = "";
    }
  }
};
</script>

<style scoped>
/* See https://stackoverflow.com/questions/19362716/how-to-style-a-html-label-for-disabled-input */
input[type="text"] {
  margin-left: 1ex;
  margin-right: 1ex;
}
input:disabled {
  background: #dddddd;
}
input:disabled + label {
  color: #ccc;
}
input[type="text"] + label {
  float: left;
}
#input-error {
  color: red;
  margin-left: 1em;
}
</style>
