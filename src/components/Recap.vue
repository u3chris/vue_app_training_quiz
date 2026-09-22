<script setup>
const props = defineProps({
    answers: Array,
    quiz: Object
})
// const correctAnswers = props.quiz.questions.map((q) => q.correct_answer)

const score = props.answers.reduce((score, currentAnswer, index) => {
        if(currentAnswer === props.quiz.questions[index].correct_answer){
            score++
        }
        return score
}, 0)

const message = (score < props.quiz.minimum_score) ? props.quiz.failure_message : props.quiz.success_message 
</script>

<template>
    <h1>Récap</h1>
    <p>Score final: {{ score }}/{{ quiz.questions.length }}</p>
    <p>{{ message }}</p>
</template>