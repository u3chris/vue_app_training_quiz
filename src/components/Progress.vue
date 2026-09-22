<script setup>
defineProps({
    value: Number,
    max: Number
})
</script>

<template>
    <div>
        <progress :value="value" :max="max"></progress>
    </div>
</template>