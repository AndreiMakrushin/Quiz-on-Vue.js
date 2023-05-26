<script setup>
    import Header from "../components/Header.vue"
    import Result from "../components/Result.vue"
    import Question from "../components/Question.vue"
    import {useRoute} from "vue-router"
    import {ref, computed} from "vue"
    import quizes from "../data/data.json"


    const route = useRoute()
    const quizid = parseInt(route.params.id)
    const quiz = quizes.find(q => q.id === quizid)
    const currentQuestionIndex = ref(0)
    const numberCorrectAnswers = ref(0)
    const showResult = ref(0)

    const questionStatus = computed(()=> `${currentQuestionIndex.value}/${quiz.questions.length}`)
    const barPercentage = computed(()=> `${currentQuestionIndex.value/quiz.questions.length*100}%`)

    const onOptionSelected = (isCorrect)=>{
        if (isCorrect) {
            numberCorrectAnswers.value++
        }
        if (quiz.questions.length -1 === currentQuestionIndex.value) {
                showResult.value = true  
        }
        currentQuestionIndex.value++
    }
</script>
<template>
    <div>
        <Header
        :questionStatus="questionStatus" 
        :barPercentage="barPercentage"
        />
        <div>
            <Question 
                v-if="!showResult" 
                :question="quiz.questions[currentQuestionIndex]" 
                @selectOption="onOptionSelected"
            />
            <Result 
                v-else 
                :showResult="quiz.questions.length" 
                :numberCorrectAnswers="numberCorrectAnswers"
        />
        </div>
        
    </div>
</template>
<style scoped>
  
</style>