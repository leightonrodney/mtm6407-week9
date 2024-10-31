<script setup>

import { ref, computed } from 'vue';

const message = ref('Hello World');

const reversedMessage = computed(() => {
    return message.value.split('').reverse().join('');
});

</script>


<template>

    <h2>Original Message: {{ message }}</h2>
    <h2>Reversed Message: {{ reversedMessage }}</h2>

    <h2>{{ reversedMessage.length }}</h2>

</template>