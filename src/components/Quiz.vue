<script setup>
import { computed, ref } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';
import Recap from './Recap.vue';

const props = defineProps({
    quiz: Object
})
const step = ref(0)
const answers = ref(props.quiz.questions.map(() => null))
const question = computed(() => {
    return props.quiz.questions[step.value]
})
const addAnswer = (answer) => {
    answers.value[step.value] = answer
    step.value++
}

</script>

<template>
    <div>
        <h1>{{ quiz.title }}</h1>
        <Progress :value="step" :max="quiz.questions.length"/>
        <Question :question="question" :step="step" v-if="question" @answer="addAnswer"/>
        <Recap v-if="step === quiz.questions.length" :answers="answers" :quiz="quiz"/>
    </div>
</template>