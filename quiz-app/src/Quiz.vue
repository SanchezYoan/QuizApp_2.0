<template>
  <div>
    <h1>{{ quiz.title }}</h1>  

    <div v-if="state='questions'">
        <Progress :value="step" :max="quiz.questions.length" />
        <Questions v-if="state === 'questions'" :key="step" :question="currentQuestion" @answer="handleAnswer"/>
        <Recap v-if="state === 'result'" :score="score" :answers="answers" :results="state === 'result' ? handleResult : 0" />
    </div>
  </div>
</template>

<script setup>
import Questions from './Questions.vue'
import Progress from './Progress.vue'
import Recap from './Recap.vue'
import { ref, computed } from 'vue'


const props = defineProps({
    quiz: Object
})

const score = ref(0)
const step = ref(0)
const state = ref('questions')
// Initialise un tableau de réponses avec null pour chaque question
const answers = props.quiz.questions.map(() => null)


const currentQuestion = computed(() => {
    return props.quiz.questions[step.value]
})

function handleAnswer(answer) {
    answers[step.value] = answer

    if (step.value >= props.quiz.questions.length - 1) {
        state.value = 'result'
    }
    step.value++
}
const handleResult = computed(() => {
    const correct_answers = props.quiz.questions.map((e) => e.correct_answer)
    correct_answers.reduce((acc, curr, index) => {
        if (curr === answers[index]) {
            score.value++
        }
    }, 0)
    return score.value
})
</script>

<style scoped>
</style>