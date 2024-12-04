<template>
  <div ref="echartsRef" style="width: 600px; height: 400px;"></div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { CanvasRenderer } from 'echarts/renderers';

// 注册必要的组件
echarts.use([BarChart, CanvasRenderer]);

const echartsRef = ref(null);
let myChart = null;

onMounted(() => {
  myChart = echarts.init(echartsRef.value);
  // 指定图表的配置项和数据
  const option = {
    xAxis: {
      type: 'category',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    },
    yAxis: {
      type: 'value'
    },
    series: [{
      data: [150, 230, 224, 218, 135, 147, 260],
      type: 'bar'
    }]
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
