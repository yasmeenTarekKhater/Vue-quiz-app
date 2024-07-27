<script setup>
import Question from '../components/Question.vue';
import QuestionHeader from '../components/QuestionHeader.vue';
import Results from '../components/Results.vue';
import { useRoute } from 'vue-router';
import quizes from '../data/quizes.json';
import { computed, ref, watch } from 'vue';

const route = useRoute();
const curentQuestionIndex=ref(0);
const numberOfCorrectAnswers=ref(0);
const showResults=ref(false);
const quizId=parseInt(route.params.id);
const quize=quizes.find(q=>q.id===quizId);

// const questionStatus=ref(`${curentQuestionIndex.value}/${quize.questions.length}`);

// watch(()=>curentQuestionIndex.value,()=>{
//     questionStatus.value=`${curentQuestionIndex.value}/${quize.questions.length}`;
// })
const questionStatus=computed(()=>`${curentQuestionIndex.value}/${quize.questions.length}`);
const barPercentage=computed(()=>`${curentQuestionIndex.value/quize.questions.length*100}%`);
const handleCorrectAnswers=(isCorrect)=>{
    if(isCorrect){
        numberOfCorrectAnswers.value++;
    }
    if(curentQuestionIndex.value===quize.questions.length-1){
        showResults.value=true;
    }
    curentQuestionIndex.value++;
}
</script>
<template>
    <QuestionHeader :questionStatus="questionStatus" :barPercentage="barPercentage"/>
    <div>
        <Question v-if="!showResults" :question="quize.questions[curentQuestionIndex]" 
        @selectOption="handleCorrectAnswers"
        />
        <Results v-else :numberOfCorrectAnswers="numberOfCorrectAnswers"
            :totalNumberOfQuestions="quize.questions.length"
        />
    </div>
</template>
