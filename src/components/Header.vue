<script setup>
    import { defineProps } from 'vue';

    const {questionStatus, barPercentage} = defineProps(["questionStatus", "barPercentage"])
</script>
<template>
    <div>
        <header>
            <h4>{{questionStatus}}</h4>
            <div class="bar">
                <div class="completion" :style="{width: barPercentage}"></div>
            </div>    
        </header>
    </div>
</template>
<style scoped>
    header{
        margin-top: 20px;
    }
    header h4 {
        font-size: 30px;
    }
    .bar{
        width: 300px;
        height: 50px;
        border: 2px solid bisque;
    }
    .completion{
        width: 0%;
        height: 100%;
        background-color: bisque;
        transition: .3s;
    }
</style>