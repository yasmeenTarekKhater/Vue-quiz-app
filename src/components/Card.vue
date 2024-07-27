<script setup>
import { useRouter } from 'vue-router';


const router=useRouter();
const {data}=defineProps(['data']);
const navigateToQuiz=()=>{
  router.push(`/quiz/${data.id}`);
}
</script>
<template>
    <div class="card" @click="navigateToQuiz">
        <img :src="data.img" :alt="data.name">
        <div class="card-text">
          <h2>{{data.name}}</h2>
          <h4>{{data.questions.length}} questions</h4>
        </div>
      </div>
</template>