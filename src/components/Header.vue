<template>
    <div>
        <b-nav tabs>
            <b-nav-item disabled>VueJs Tutorial Quiz</b-nav-item>
            <b-nav-item disabled>Counter: {{numCorrectAnswers}}/{{totalAnswers}}</b-nav-item>
        </b-nav>
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