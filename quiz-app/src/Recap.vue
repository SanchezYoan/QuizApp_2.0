<template>
    <div>
        <h1>Récapitulatif</h1>
        <p>Score: {{ score }}/{{ answers.length }}</p>
        <h4 v-if="score / answers.length > 0.5">Bravo!</h4>
        <h4 v-else>Try again!</h4>
    </div>
</template>

<script setup>
const props = defineProps({
    answers: Array,
    score: Number
})

console.log(props.score)
console.log(props.answers)
</script>

<style scoped>
</style>