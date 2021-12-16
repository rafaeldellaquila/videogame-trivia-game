<template>
  <div>
    <template v-if="this.question">
      <h1 v-html="this.question" />

      <template v-for="(answer, indice) in this.answers" :key="indice">
        <input
          type="radio"
          :id="indice"
          name="options"
          :value="answer"
          v-model="this.chosenAnswer"
        />
        <label :for="indice" v-html="answer" />
        <br />
      </template>
    </template>

    <button class="send" type="button" @click="submitAnswer()">Send</button>
  </div>
</template>

<script>
//
export default {
  name: 'App',

  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
      chosenAnswer: undefined
    }
  },

  methods: {
    submitAnswer() {
      if (!this.chosenAnswer) {
        alert('Pick one of the options')
      } else {
        if (this.chosenAnswer == this.correctAnswer) {
          alert('You got it right!')
        } else {
          alert('You got it wrong!')
        }
      }
    }
  },

  computed: {
    answers() {
      const answers = JSON.parse(JSON.stringify(this.incorrectAnswers))
      answers.splice(
        Math.round(Math.random() * answers.length),
        0,
        this.correctAnswer
      )
      return answers
    }
  },

  created() {
    this.axios
      .get('https://opentdb.com/api.php?amount=1&category=15')
      .then((response) => {
        const data = response.data.results[0]
        this.question = data.question
        this.incorrectAnswers = data.incorrect_answers
        this.correctAnswer = data.correct_answer
      })
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type='radio'] {
    margin: 12px 4px;
  }

  .send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: white;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }
}
</style>
