<template>
  <div>
    <h1>{{ quiz.title }}</h1>  

    <div v-if="state='questions'">
        <Progress :value="step" :max="quiz.questions.length" />
        <Questions :question="currentQuestion" :key="step" @change="handleAnswer" />
    </div>
  </div>
</template>

<script setup>
import Questions from './Questions.vue'
import Progress from './Progress.vue'
import { ref, computed } from 'vue'


const props = defineProps({
    quiz: Object
})

const step = ref(0)
const state = ref('questions')
// Initialise un tableau de réponses avec null pour chaque question
const answers = props.quiz.questions.map(() => null)

const currentQuestion = computed(() => {
    return props.quiz.questions[step.value]
})

function handleAnswer(answer) {
    model.value[step.value] = model.value
    step.value++
}
</script>

<style scoped>
</style>