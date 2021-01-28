<template>
  <div id="add-group">
    <input
      @focus="focus"
      @blur="blurs"
      :class="isFocus === true ? 'input_focus' : ''"
      type="text"
      placeholder="请输入任务标题"
    />
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  props: ["inputValue"],
  setup() {
    let isFocus = ref(false);
    return {
      isFocus,
    };
  },
  methods: {
    blurs() {
      this.isFocus = false;
    },
    focus() {
      this.isFocus = true;
    },
    // mouseEnter() {
    //   this.isFocus = true;
    // },
    // mouseLeave() {
    //   this.isFocus = false;
    // },
  },
};
</script>
<style scoped>
input {
  outline: none;
  width: 190px;
  height: 35px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  padding: 4px;
  margin: 4px;
}
.input_focus {
  border-color: rgba(0, 0, 0, 0.3);
}
</style>
