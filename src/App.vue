<template>
  <div class="calendar-demo">
    <van-cell-group inset>
      <van-cell title="选择时间区间" :value="value" is-link @click="show=true" /> 
    </van-cell-group>
    <van-calendar
      v-model:show="show"
      type="range"
      :allow-same-day="false"
      :formatter="dayFormatter"
      @confirm="handleConfirm"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";

const show = ref(false);
const value = ref('')
const handleConfirm = (days) => {
  const [start, end] = days
  value.value = `${start.getMonth()+1}月${start.getDate()}日 - ${start.getMonth()+1}月${end.getDate()}日`
  show.value = false
}
const dayFormatter = (day) => {
  if (!day.date) {
    return day;
  }

  const date = day.date.getDate();

  if (date > 14 && date < 23 && date % 2 !== 0) {
    day.type = "disabled";
  }

  if (day.type === "start") {
    day.bottomInfo = "开始";
  } else if (day.type === "end") {
    day.bottomInfo = "结束";
  }

  return day;
};

</script>

<style>
body {
  background-color: aliceblue;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
