<script setup>
import Card from "../components/Card.vue"
  import q from "../data/data.json"
  import {ref, watch} from "vue"
  import gsap from "gsap"

  const quizes = ref(q)
  
  const searchQuiz = ref('')

  watch(searchQuiz, ()=>{
    quizes.value = q.filter(quiz=> quiz.name.toLowerCase().includes(searchQuiz.value.toLowerCase()))
  })
  const afterEnter = (el)=>{
  }
  const beforeEnter = (el) =>{
    el.style.opacity = 0;
    el.style.transform = "translateY(-50px)";
  }
  const enter = (el) =>{
    gsap.to(el, {
      y: 0,
      opacity: 1,
      duration: 0.9,
      delay: el.dataset.index * 0.3
    })
    
  }
</script>
<template>
  
    <header>
      <h1>Тесты</h1>
      <input type="text" placeholder="Найти тест" v-model.trim="searchQuiz">
    </header>
    <div class="options-container">
      <TransitionGroup 
      name="card" 
      appear 
      @after-enter="afterEnter"
      @before-enter="beforeEnter"
      @enter="enter"
      >
        <Card 
        v-for="(quiz, index) in quizes" 
        :key="quiz.id" 
        :quiz="quiz"
        :data-index="index"
        />
      </TransitionGroup>
    </div>
  
</template>

<style scoped>
  header {
    margin-bottom: 10px;
    margin-top: 30px;
    display: flex;
    align-items: center;
  }

  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }

  header input {
    border: none;
    background-color: rgba(128,128,128,0.1);
    padding: 10px;
    border-radius: 5px;
  }

  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  } 

/*.card-enter-from{
  transform: translateY(-50px);
  opacity: 0;
}
.card-enter-to{
  transform: translateY(0);
  opacity: 1;
}
.card-enter-active{
  transition: all .4s ease;
}*/
</style>