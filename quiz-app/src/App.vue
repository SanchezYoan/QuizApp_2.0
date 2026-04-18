<script setup></script>

<template>
  <div v-if="state=== 'loading'">
    Chargement...
  </div>
  <div v-else-if="state=== 'error'">
    Erreur
  </div>
  <div v-else-if="state=== 'idle'">
    <Quiz :quiz="quiz"/>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Quiz from './Quiz.vue'
const state = ref('loading')
const quiz = ref(null)
const url = '/quiz.json'

onMounted(() => {
  fetch(url)
    .then(r => {
      if (r.ok) {
        return r.json()
      }
      throw new Error('Impossible de charger le questionnaire')
    
    }).then(data => {
      quiz.value = data
      state.value = 'idle'
    })
    .catch(err => {
      console.error(err)
      state.value = 'error'
    })
})
</script>

<style scoped></style>
