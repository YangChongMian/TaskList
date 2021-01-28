<template>
  <div id="add-group">
    <div>
      <Input v-model="value" />
      <Button @click="addTask" :btnName="data.btnName" />
    </div>
  </div>
</template>

<script>
import Input from "../components/Input.vue";
import Button from "../components/Button.vue";
import { reactive, ref, toRef } from "vue";
export default {
  props:['value'],
  components: {
    Input,
    Button,
  },
  setup() {
    let data = reactive({
      isFocus: false,
      value: "11111",
      btnName: "添加新任务",
    });
    // let btnName = toRef(data, "btnName");
    let blurs = function () {
      this.isFocus = false;
    };
    let focus = function () {
      this.isFocus = true;
    };
    function addTask(){
        console.log(data.value);
    }
    return {
      data,
      blurs,
      focus,
      addTask
    //   btnName,
    };
  },
  methods: {},
};
</script>
<style scoped>
#add-group>div{
    display: flex;
}
</style>
