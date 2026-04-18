<template>
    <div>
        <h1>Résultat</h1>
        <p>Score: {{ score }}/{{ answers.length }}</p>
        <h3 class="success" v-if="score / answers.length > 0.5">{{success}}</h3>
        <h3 class="failure" v-else>{{failure}}</h3>
        <button @click="restart">Recommencer</button>
    </div>
</template>

<script setup>
const props = defineProps({
    answers: Array,
    score: Number,
    success: String,
    failure: String
})

const emits = defineEmits(['restart'])

const restart = () => {
    emits('restart')
}

console.log(props.score)
console.log(props.answers)
</script>

<style scoped>
.success {
    color: green;
}
.failure {
    color: red;
}
</style>