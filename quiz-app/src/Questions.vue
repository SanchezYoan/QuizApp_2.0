<template>
    <div class="card">
        <ul>
            <h2 class="question-title">{{ props.question.question }}</h2>
            <li class="card-item" v-for="(choice, index) in props.question.choices" :key="choice">
               <Answer :value="choice" @change="handleAnswer" :id="`answer-${index}`" :correct_answer="props.question.correct_answer" :disabled="hasAnswer" v-model="answer" />
            </li>
            <button @click="onValidate" :disabled="!hasAnswer">Question suivante</button>
        </ul>
    </div>
</template>

<script setup>
import { ref, defineEmits, computed, watch, onMounted } from 'vue'
import Answer from './Answer.vue'

const randomChoices = ref([])

const props = defineProps({
    question: Object
})

onMounted(() => {
    randomChoices.value = props.question.choices.sort(() => Math.random() - 0.5)
})

const answer = ref(null)
const selectedAnswer = ref(null)
const emits = defineEmits(['answer'])

const onValidate = () => {
    emits('answer', selectedAnswer.value)
}

const handleAnswer = (answer) => {
    selectedAnswer.value = answer.target.value
    // console.log(answer.target.value)
}

const hasAnswer = computed(() => {
    return answer.value !== null
})
</script>

<style scoped>
.card {
    margin: 2rem;
}
button {
    display: block;
    margin-left: auto;
}

.question-container {
    margin: 0 1rem;
}

ul li {
    list-style: none;
}
</style>

