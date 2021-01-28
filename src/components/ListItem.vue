<template>
  <div id="item-container">
    <slot name="closeIcon"></slot>
    <section>
      <h3>{{ index }}、{{ title }}</h3>
    </section>
    <section>
      <slot name="details"></slot>
    </section>
    <section class="times">
      <slot name="timeType"></slot>
      <span class="date">{{ timer }}</span>
    </section>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "",
    },
    timer: {
      type: String,
      default: "",
    },
    index:{
      type:Number
    }
  },
  setup(props,{ emit }){

    function finishTask(){
      emit('finishTask')
    }
    return {
      finishTask
    }
  },
};
</script>
<style scoped>
#item-container {
  position: relative;
  margin: 10px auto;
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  box-shadow: rgb(204, 204, 204) -2px 2px 20px 0px;
  border-radius: 6px;
}
.times {
  display: flex;
  justify-content: flex-end;
  align-items: baseline;
  font-size: 14px;
  color: #777;
}
.times > span.date{
  font-size: 12px;
  margin-left:4px;
}
</style>
