<template>
  <div id="main" style="width: 600px; height: 400px;"></div>
</template>

<script setup lang="ts">
import * as echarts from 'echarts';

let chartDom = document.getElementById('main');
let myChart = echarts.init(chartDom);
let option;

option = {
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

option && myChart.setOption(option);

</script>

<style scoped>
/* 可以在这里添加一些样式 */
</style>
