<script setup>
    import {defineProps} from "vue"
    import {useRouter} from "vue-router"
    const {showResult, numberCorrectAnswers} = defineProps(["showResult","numberCorrectAnswers"])
    const router = useRouter()
    
</script>
<template>
    <div class="container">
        <div class="block-result">
            Ответили правильно на {{ numberCorrectAnswers }} из {{ showResult }} вопросов
        </div>
        <div class="block-back">
            <button @click="router.push(`/`)">Вернуться на главную страницу</button>
        </div>
    </div>
</template>
<style scoped>
    .container{
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #b5b5b5;
    }
    .block-result{
        font-size: 20px;
        transition: 3s;
    }
</style>