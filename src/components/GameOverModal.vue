<template>
<div id="gameOverModalWrapper">  
    <b-modal id="game-over-modal" no-footer @hidden="resetGame" ok-only title="Thank you for playing!" ok-title="Reset">
    <div id="playerResults">
        <span class="totalAnswersMessage">Your score: {{numCorrectAnswers}}/{{totalAnswers}}</span>
    </div>
    <div id="gameResetMessage">
        Please click "Reset" below to restart the quiz
    </div>
    </b-modal>
</div>
</template>

<script>
export default {
    props: [
        'numCorrectAnswers',
        'totalAnswers',
        'resetGame'
    ]   
}
</script>

<style scoped>
    .navbar-wrapper {
        background: #F7F7F7;
    }
    #quizTitleText {
        color: #000000;
    }
    .totalAnswersMessage {
        color: #000000;
    }
</style>