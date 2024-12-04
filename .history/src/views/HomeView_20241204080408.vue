<template>
  <div ref="echartsRef" style="width: 600px; height: 400px;"></div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { CanvasRenderer } from 'echarts/renderers';

// 注册必要的组件
echarts.use([BarChart, CanvasRenderer]);

const echartsRef = ref(null);
let myChart = null;

onMounted(() => {
  myChart = echarts.init(echartsRef.value, null, { renderer: 'canvas' });
  // 指定图表的配置项和数据
  const option = {
    tooltip: {
      trigger: 'axis',
      axisPointer: { type: 'shadow' }
    },
    legend: {
      data: ['销量']
    },
    xAxis: {
      type: 'category',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    },
    yAxis: {
      type: 'value'
    },
    series: [
      {
        name: '销量',
        type: 'bar',
        data: [120, 200, 150, 80, 70, 110, 130],
        emphasis: {
          itemStyle: {
            shadowBlur: 10,
            shadowOffsetX: 0,
            shadowColor: 'rgba(0, 0, 0, 0.5)'
          }
        }
      }
    ]
  };

  // 使用刚指定的配置项和数据显示图表。
  myChart.setOption(option);
});

// 在组件卸载时，销毁图表实例
onBeforeUnmount(() => {
  if (myChart != null) {
    myChart.dispose();
  }
});
</script>

<style scoped>
/* 可以在这里添加一些样式 */
</style>
