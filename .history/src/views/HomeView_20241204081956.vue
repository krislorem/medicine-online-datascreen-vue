<template>
  <div id="m" style="width: 600px; height: 400px;"></div>
</template>

<script setup lang="ts">
import * as echarts from 'echarts';
import { onMounted } from 'vue'


const option = {
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [150, 230, 224, 218, 135, 147, 260],
      type: 'line'
    }
  ]
};
onMounted(() => {
  let chartDom = document.getElementById('m');
  let myChart = echarts.init(chartDom);
  option && myChart.setOption(option);
})


</script>

<style scoped>
/* 可以在这里添加一些样式 */
</style>
