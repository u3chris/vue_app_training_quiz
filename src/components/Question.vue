<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
    question: Object,
    step: Number
})
const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)
const sendAnswer = () => {
    emits('answer', answer.value)
    answer.value = null
}
</script>

<template>
    <div class="question">
        <h3>{{ step + 1}}) {{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in question.choices" :key="choice">
                <label :for="`answer${index}`">
                    <input type="radio" name="answer" :id="`answer${index}`" v-model="answer" :value="choice">
                    {{ choice }}
                </label>
            </li>
        </ul>
        <button :disabled="!hasAnswer" @click="sendAnswer">Question suivante</button>
    </div>
</template>

<style scoped>
.question {
    padding-top: 2rem;
}
.question button {
    margin-left: auto;
    display: block;
}
</style>