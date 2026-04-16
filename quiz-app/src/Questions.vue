<template>
    <div>
        <ul>
            <h2>{{ props.question.title }}</h2>
            <li v-for="(choice, index) in props.question.choices" :key="choice">
               <Answer :value="choice" :id="`answer-${index}`" :correct_answer="props.question.correct_answer" :disabled="hasAnswer" v-model="answer" />
            </li>
            <button @click="emits('answer', answer)" :disabled="!hasAnswer">Question suivante</button>
        </ul>

    </div>
</template>

<script setup>
import { ref, defineEmits, computed } from 'vue'
import Answer from './Answer.vue'

const props = defineProps({
    question: Object
})
const answer = ref(null)
const emits = defineEmits(['change'])

const hasAnswer = computed(() => {
    return answer.value !== null
})
</script>

<style scoped>

</style>

