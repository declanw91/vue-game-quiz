<template>
  <div id="app">
    <Header :numCorrectAnswers="numCorrectAnswers" :totalAnswers="totalAnswers"/>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox 
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :nextQuestion="nextQuestion"
            :increment="increment"
            :totalAnswers="totalAnswers"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrectAnswers: 0,
      totalAnswers: 0
    }
  },
  methods:{
    nextQuestion: function() {
      this.index++;
    },
    increment: function(isCorrect) {
      if(isCorrect) {
        this.numCorrectAnswers++;
      }
      this.totalAnswers++;
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=15&type=multiple', {
      method: 'GET'
    }).then((response) => {
       return response.json();
    }).then((jsonData) => {
      this.questions = jsonData.results;
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-image: url("/img/game-icons-background.png");
  background-repeat: repeat, repeat;
}
</style>
