<script setup>
import { ref, watch } from 'vue';
import Card from '../components/Card.vue';
import quizesData from '../data/quizes.json';

const data=ref(quizesData);
const searchValue=ref('');

watch(searchValue,()=>{
  data.value=quizesData.filter(quiz=>quiz.name.toLowerCase().includes(searchValue.value.toLowerCase()))
})
</script>
<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="searchValue" type="text" placeholder="Search...">
    </header>
    <div v-if="data.length > 0" class="options-container">
      <Card v-for="quiz in data" :key="quiz.id" :data="quiz"/>
    </div>
    <div v-else>
      <h2 style="text-align: center;">No quizes found .....</h2>
    </div>
  </div>
</template>