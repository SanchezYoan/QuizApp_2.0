<template>
    <div>
        <progress :value="value" :max="max"/>
        <h4>{{ value }}/{{ max }}</h4>
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
