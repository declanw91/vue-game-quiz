<template>
<div class="navbar-wrapper">
  <b-navbar toggleable="lg" type="dark">
    <b-navbar-brand href="#">
        <img alt="Quiz Logo" src="/img/game-controller-icon.png" width="50">
        <span id="quizTitleText">Video Game Quiz Time!</span>
    </b-navbar-brand>
    <b-nav-text><span class="totalAnswersMessage">Correct Answers: {{numCorrectAnswers}}/{{totalAnswers}}</span></b-nav-text>
  </b-navbar>
</div>
</template>

<script>
export default {
    props: [
        'numCorrectAnswers',
        'totalAnswers'
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