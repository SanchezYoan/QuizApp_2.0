<template>
    <div>
        <h2>Progress</h2>
        <progress :value="value" :max="max"/>
        <h4>{{ value + 1 }}/{{ max }}</h4>
    </div>
</template>

<script setup>

defineProps({
    value: Number,
    max: Number
})
</script>

<style scoped>
</style>
