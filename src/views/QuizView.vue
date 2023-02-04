<script setup>
    import Question from "../components/Question.vue"
    import QuizHeader from "../components/QuizHeader.vue"
    import Result from "../components/Result.vue"
    import { useRoute } from "vue-router";
    import { ref, watch, computed } from "vue";
    import quizes from "../data/quizes.json"

    const route = useRoute()
    const quizid = parseInt(route.params.id)
    const quiz = quizes.find(q=>q.id === quizid)
    const correntQuestionIndex = ref(0)
    const numberOfCorrectAnswers = ref(0)
    const showResults = ref(0)
    
    const questionStatus = computed(()=> `${correntQuestionIndex.value}/${quiz.questions.length}`)
    const barPercentage = computed(() => `${correntQuestionIndex.value/quiz.questions.length * 100}%`)

    const onOptionSelected = (isCorrect) =>{
        if (isCorrect) {
            numberOfCorrectAnswers.value++
        }
        if (quiz.questions.length- 1 === correntQuestionIndex.value) {
            showResults.value = true
        }
        correntQuestionIndex.value++
    }
</script>
<template>
    <div>
        <QuizHeader
         :questionStatus="questionStatus"
         :barPercentage="barPercentage"
         />
        <div>
            <Question 
            v-if="!showResults"
            :question="quiz.questions[correntQuestionIndex]"
            @selectOption="onOptionSelected"
            />
        </div>
        <Result 
        :showResults="quiz.questions.length"
        :numberOfCorrectAnswers="numberOfCorrectAnswers"
        />
    </div>
</template>

