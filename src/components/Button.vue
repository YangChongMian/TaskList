<template>
  <div id="add-group">
    <button @mousedown="clickDown" @mouseup="clickUp" :class="mouseDown === true ? 'mouse-down' : ''">{{ btnName }}</button>
  </div>
</template>

<script>
import { computed, ref } from "vue";
export default {
    props:['btnName'],
    setup() {
        let mouseDown = ref(false);
        
        function clickDown(){
            mouseDown.value = true
        }
        function clickUp(){
            mouseDown.value = false
        }
        return {
            mouseDown,clickDown,clickUp
        };
    },
};
</script>
<style scoped>
button {
  outline: none;
  min-width: 60px;
  height: 35px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  padding:4px;
  margin:4px;
  cursor:pointer;
}
.mouse-down {
  background-color: rgba(0,0,0,.1);
}
</style>
