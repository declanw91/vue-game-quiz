<template>
    <div class="question-box-wrapper">
        <b-jumbotron>

            <template v-slot:lead>
             <span v-html="currentQuestion.question"></span>
            </template>

            <hr class="my-4">

            <b-list-group>
                <b-list-group-item :class= "answerClass(index)" v-for="(answer, index) in shuffledAnswers" :key="index" @click="selectAnswer(index)">
                    <span v-html="answer"></span>
                    </b-list-group-item>
            </b-list-group>

            <b-button variant="primary"
            v-on:click="submitAnswer" :disabled="selectedIndex === null || answered">Submit</b-button>
            <b-button @click="nextQuestion" variant="success" href="#" :disabled="!answered || this.totalAnswers >= 10">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash';
export default {
    props: {
        currentQuestion: Object,
        nextQuestion: Function,
        increment: Function,
        totalAnswers: Object
    },
    data(){
        return {
            selectedIndex: null,
            shuffledAnswers: [],
            answered: false,
            correctIndex: null
        }
    },
    computed: {
        answers: function() {
            let answers = [...this.currentQuestion.incorrect_answers];
            answers.push(this.currentQuestion.correct_answer);
            return answers;
        }
    },
    watch: {
        currentQuestion: {
            immediate: true,
            handler: function() {
                this.selectedIndex = null;
                this.answered = false;
                this.shuffleAnswers();
            }
        }
    },
    methods: {
        selectAnswer: function(index){
            this.selectedIndex = index;
        },
        shuffleAnswers: function() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
            this.shuffledAnswers = _.shuffle(answers);
            let correctAnswer = this.currentQuestion.correct_answer;
            this.correctIndex = this.shuffledAnswers.indexOf(correctAnswer);
        },
        submitAnswer: function() {
            let isCorrect = false;
            if(this.selectedIndex === this.correctIndex) {
                isCorrect = true;
            }
            this.answered = true;
            this.increment(isCorrect)
        },
        answerClass: function(index) {
            let answerClass = '';
            if(!this.answered && this.selectedIndex === index ) {
                answerClass = 'selectedAnswer';
            } else if (this.answered && this.correctIndex === index) {
                answerClass = 'correctAnswer';
            } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
                answerClass = 'incorrectAnswer';
            } 
            return answerClass;
        }
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }
    .list-group-item:hover {
        background: #EEEEEE;
        cursor: pointer;
    }
    .btn {
        margin: 0 5px;
    }
    .selectedAnswer {
        background: lightblue;
    }
    .correctAnswer {
        background: lightgreen;
    }
    .incorrectAnswer {
        background: #FF0000;
    }
    .question-box-wrapper {
        margin-top: 10px;
    }
</style>