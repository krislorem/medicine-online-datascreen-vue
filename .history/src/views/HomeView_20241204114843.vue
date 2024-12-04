<template>
  <div class="home">
    <nav>
      <h1>中医在线考核可视化大屏</h1>
    </nav>
    <div id="mid-bar">
      <select id="info"></select>
    </div>
    <div id="all-info">
      <div id="left">
        <div class="item item-1">
          <p class="top-name"><span>考核信息</span></p>
          <p class="time-title"><span>考试已经结束</span></p>
          <div class="time-container">
            <div class="time-box" style=";"><span class="time-num">561</span></div>
            <div class="time-box" style=";"><span class="time-num">天</span></div>
            <div class="time-box" style=";"><span class="time-num">11</span></div>
            <div class="time-box" style=";"><span class="time-num">小时</span></div>
            <div class="time-box" style=";"><span class="time-num">12</span></div>
            <div class="time-box" style=";"><span class="time-num">分钟</span></div>
            <div class="time-box" style=";"><span class="time-num">08</span></div>
            <div class="time-box" style=";"><span class="time-num">秒</span></div>
          </div>
        </div>
      </div>
      <div id="right"></div>
    </div>
  </div>
</template>

<style scoped>
body {
  font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB, Microsoft YaHei, "\5FAE\8F6F\96C5\9ED1", Arial, sans-serif;
  font-size: 12px;
  line-height: 1.5;
  color: #515a6e;
  background-color: #fff;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.home {
  background: #010152 url(/ditu.png) 50% no-repeat;
  background-size: 100% 100%;
}

.home nav {
  background-image: url(/dingbu.png);
  background-size: 100% 100%;
  background-repeat: no-repeat;
  overflow: hidden;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}

.home nav h1 {
  font-size: 30px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #fff;
  line-height: 58px;
  letter-spacing: 5px;
  margin: 15px auto;
}

.home #mid-bar {
  width: 694px;
  height: 43px;
  background: url(/nav.png) no-repeat;
  margin: 48px auto 36px;
  padding-top: 12px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}

.home #mid-bar #info {
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
  background: transparent url('/jiantou.png') no-repeat scroll 100%;
  width: 302px;
  height: 22px;
  font-size: 16px;
  text-align: center;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #26c5fb;
  line-height: 22px;
  letter-spacing: 2px;
  border: none;
}

#all-info {
  width: 100%;
  height: 796px;
  margin: 20px auto;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-pack: distribute;
  justify-content: space-around;
}
</style>
<script setup lang="ts">
import * as echarts from 'echarts';
import { onMounted } from 'vue'
const labelOption = {
  show: true,
  position: 'insideBottom',
  distance: 15,
  align: 'left',
  verticalAlign: 'middle',
  rotate: 90,
  formatter: '{c}  {name|{a}}',
  fontSize: 16,
  rich: {
    name: {}
  }
};
const option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'shadow'
    }
  },
  legend: {
    data: ['Forest', 'Steppe', 'Desert', 'Wetland']
  },
  xAxis: [
    {
      type: 'category',
      axisTick: { show: false },
      data: ['2012', '2013', '2014', '2015', '2016']
    }
  ],
  yAxis: [
    {
      type: 'value'
    }
  ],
  series: [
    {
      name: 'Forest',
      type: 'bar',
      barGap: 0,
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: [320, 332, 301, 334, 390]
    },
    {
      name: 'Steppe',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: [220, 182, 191, 234, 290]
    },
    {
      name: 'Desert',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: [150, 232, 201, 154, 190]
    },
    {
      name: 'Wetland',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: [98, 77, 101, 99, 40]
    }
  ]
};
onMounted(() => {
  let chartDom = document.getElementById('m');
  let myChart = echarts.init(chartDom);
  option && myChart.setOption(option);
})


</script>

