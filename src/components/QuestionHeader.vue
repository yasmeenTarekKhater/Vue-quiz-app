<script setup>
    defineProps({
        questionStatus:String,
        barPercentage:String
    })
</script>
<template>
    <div >
        <h1>Question {{ questionStatus }}</h1>
        <div class="bar">
            <div class="completion" :style="{width:barPercentage}"></div>
        </div>
    </div>
</template>