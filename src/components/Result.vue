<script setup>
import { defineProps } from 'vue';

const {showResults, numberOfCorrectAnswers} = defineProps(["showResults", "numberOfCorrectAnswers"])
</script>
<template>
    <div class="results">
    <h1>Ваш результат</h1>
    <h1>{{ numberOfCorrectAnswers +"/"+ showResults }}</h1>
    </div>
</template>

<style scoped>
    .results{
        text-align: center;
        padding: 100px 0;
    }
    h1{
        font-size: 50px;
    }
</style>