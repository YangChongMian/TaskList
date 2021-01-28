<template>
    <div id="title">
        {{ pageTitle }}
    </div>
</template>
<script>
import { ref } from 'vue'
export default {
    setup(){
        const pageTitle = ref('我的任务')
        return {
            pageTitle
        }
    }
}
</script>
<style scoped>
#title{
    height: 60px;
    text-align: center;
    width: 100%;
    line-height: 60px;
    font-size: 20px;
    box-shadow: 2px 2px 5px #ccc;
}
</style>