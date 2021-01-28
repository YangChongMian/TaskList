<template>
  <div>
    <Header />

    <section id="add-group">
      <!-- <Input v-model="inputValue" /> -->
      <input
        type="text"
        placeholder="任务标题"
        v-model="state.inputValue"
      />
      <input
        type="text"
        placeholder="任务说明"
        v-model="state.taskDetail"
      />
      <Button @click="addTask" :btnName="state.btnName" />
    </section>
    <div id="list">
      <section id="task">
        <h2>未完成列表</h2>
        <span v-if="state.taskList.length === 0">您还没有未完成的任务</span>
        <Item
          v-else
          v-for="(item, index) in state.taskList"
          :key="index"
          :title="item.title"
          :timer="item.time"
          :index="index + 1"
        >
          <template #timeType>
            <span>开始：</span>
          </template>
          <template #closeIcon>
            <span @click="finishTask(item, index)" class="iconfont icon-quxiao"></span>
          </template>
          <template #details>
            <p>{{ item.details }}</p>
          </template>
        </Item>
      </section>
      <section id="finished">
        <div class="finish_title">
          <h2>完成历史列表</h2>
          <Button class="btn" @click="clearHistory" :btnName="'清空历史'"></Button>
        </div>
        <span v-if="state.historyList.length === 0">您还没有已完成的任务</span>
        <Item
          v-else
          v-for="(item, index) in state.historyList"
          :key="index"
          :title="item.title"
          :timer="item.time"
          :index="index + 1"
        >
          <template #timeType>
            <span>结束：</span>
          </template>
          <template #details>
            <p>{{ item.details }}</p>
          </template>
        </Item>
      </section>
    </div>
  </div>
</template>

<script>
import Header from "./components/PageTitle.vue";
import Item from "./components/ListItem.vue";
import Button from "./components/Button.vue";
import { reactive, onMounted, onUpdated } from "vue";

export default {
  name: "App",
  components: {
    Header,
    Item,
    Button,
  },
  setup() {
    const state = reactive({
      btnName: "添加新任务", // 按钮名
      inputValue: "", // 输入框的值
      taskDetail:'', // 任务说明，可不填
      details: "hahahah",
      taskList: [], // 未完成列表
      historyList: [], // 历史列表
    });

    onMounted(() => {
      let localData = localStorage.getItem("vue3_task_list");
      state.taskList = JSON.parse(localData);
      let localDataFinished = localStorage.getItem("vue3_task_finished");
      state.historyList = JSON.parse(localDataFinished);
    });
    onUpdated(()=>{
      localStorage.setItem('vue3_task_finished',JSON.stringify(state.historyList))
    })
    return {
      state,

      // 事件列表
      addTask,  // 添加一条任务
      finishTask, // 点击完成一条任务
      clearHistory, // 清空历史列表
    };
    function addTask() {
      let date = new Date().toLocaleString();
      state.taskList.push({ title: state.inputValue, details:state.taskDetail, time: date });
      let data = JSON.stringify(state.taskList);
      localStorage.setItem("vue3_task_list", data);
      state.inputValue = "";
      state.taskDetail = "";
    }
    function finishTask(item, index) {
      console.log(index);
      let date = new Date().toLocaleString()
      item.time = date
      let localData = localStorage.getItem("vue3_task_list");
      let list = JSON.parse(localData);
      state.historyList.push(...list.splice(index, 1));
      state.taskList = list
      localStorage.setItem("vue3_task_list",JSON.stringify(state.taskList));
    }
    function clearHistory(){
      localStorage.setItem('vue3_task_finished',[])
      state.historyList = []
    }
  },
};
</script>
<style scoped>
.finish_title{
  position: relative;
}
.finish_title>.btn{
  position: absolute;
  right:10px;
  top:-6px;
}
.iconfont {
  font-size: 16px;
  position: absolute;
  right: 10px;
  top: 10px;
  /* font-weight: bold; */
  color: #777;
  cursor: pointer;
}
#list {
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  display: flex;
}
#list > section {
  width: 50%;
  box-sizing: border-box;
  padding: 10px;
}
#list > section > span,
#list > section > p {
  text-align: center;
}
#add-group {
  display: flex;
}
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
