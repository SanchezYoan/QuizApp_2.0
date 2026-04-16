<template>
    <input type="radio" :id="id" :value="value" :disabled="disabled" v-model="model" />
    <label :for="id" :class="classes">
        {{ value }}
    </label>
</template>

<script setup>

import { computed } from 'vue'

const model = defineModel()

const props = defineProps({
    value: String,
    id: String,
    correct_answer: String,
    disabled: Boolean
})

const classes = computed(() => ({
    disabled: props.disabled,
    wrong: props.disabled && props.value !== props.correct_answer && props.value === model.value,
    right: props.disabled && props.value === props.correct_answer
}))
</script>

<style scoped>

.disabled {
    opacity: 0.5;
}

.right {
    opacity: 1;
    color: green;
}

.wrong {
    opacity: 1;
    color: red;
}
</style>