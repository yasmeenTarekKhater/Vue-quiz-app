<script setup>
defineProps({
    question:Array,
});
const emit =defineEmits(['selectOption']);
const handleSelectedOption=(isCorrect)=>{
    emit('selectOption',isCorrect)
}
</script>
<template>
    <div class="question-container">
            <h1 class="question"> {{  question.text }}</h1>
        </div>
        <div class="questions-options-container">
            <div class="option" v-for="option in question.options"
                :key="option.id"
                @click="handleSelectedOption(option.isCorrect)">
                <p class="option-label">{{ option.label  }}</p>
                <div class="option-value">
                    <p> {{ option.text }}</p>
                </div>    
            </div>
        </div>
</template>