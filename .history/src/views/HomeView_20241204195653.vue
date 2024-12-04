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
          <div class="result">
            <div class="ivu-carousel" style="height: 100%;">

            </div>
            <div class="ivu-carousel-list">
              <div class="ivu-carousel-track higher"
                style="width: 119px; transform: translate3d(0px, 0px, 0px); transition: transform 500ms; visibility: visible;">
                <div class="ivu-carousel-item" style="width: 119px; height: auto; left: 0px;">
                  <div class="res-topbar">
                    <span>{{ }}</span>
                    <span>{{ }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="item item-2">
          <p class="top-name i2-top"><span>学员信息</span></p>
          <div class="i2">
            <div class="box">
              <p class="num bg-lg-blue">1</p>
              <p class="title bg-lg-blue">应考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">0</p>
              <p class="title bg-lg-cyan">签到人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">0</p>
              <p class="title bg-lg-red">实考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue">0</p>
              <p class="title bg-lg-blue">分配试卷</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">0</p>
              <p class="title bg-lg-cyan">答题中</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">0</p>
              <p class="title bg-lg-red">完成考试</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue2">1</p>
              <p class="title bg-lg-blue2">未签到</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan2">1</p>
              <p class="title bg-lg-cyan2">未考核</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red2">0</p>
              <p class="title bg-lg-red2">合格人数</p>
            </div>
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

#all-info #left {
  width: 23%;
  height: 100%;
}


#all-info #left .item {
  height: 44%;
  width: 100%;
  padding: 10px;
  background-image: url(/kuang2.png);
  background-size: 100% 100%;
}

#all-info #left .item .top-name>span {
  width: 64px;
  height: 20px;
  font-size: 14px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #26c5fb;
  line-height: 20px;
  letter-spacing: 1px;
}

#all-info #left .item-1 {
  margin-bottom: 20px;
}

#all-info #left .item-1 .time-title {
  text-align: center;
  font-size: 20px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #fff;
  line-height: 20px;
  letter-spacing: 1px;
  margin: 32px auto 28px;
}

#all-info #left .item-1 .time-container {
  height: 60px
}

#all-info #left .item-1 .time-container,
#all-info #left .item-1 .time-container .time-box {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
}

#all-info #left .item-1 .time-container .time-box {
  background-image: url('/kuang3.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  background-color: #d7606b;
}

#all-info #left .item-1 .time-container .time-box .time-num {
  font-size: 20px;
  padding: 6px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #60fffd
}

#all-info #left .item-1 .time-container .time-box .dupunkto {
  font-size: 28px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #60fffd
}

#all-info #left .item-1 .result {
  width: 100%;
  height: 43%;
  background-image: url('/kuang4.png');
  background-size: 100% 100%;
  margin: 30px auto 0;
  font-size: 16px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #fff;
  line-height: 22px;
}

#all-info #left .item-1 .result .res-sub-title {
  width: 100%;
  height: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  font-size: 20px;
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600
}

#all-info #left .item-1 .result .res-topbar {
  height: 47px;
  border-bottom: 1px solid #1e266e;
  -webkit-box-align: end;
  -ms-flex-align: end;
  align-items: flex-end;
  padding: 0 19px 5px 14px
}

#all-info #left .item-1 .result .res-box,
#all-info #left .item-1 .result .res-topbar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between
}

#all-info #left .item-1 .result .res-box {
  height: 57px;
  margin: 27px 13px 0
}

#all-info #left .item-1 .result .res-box .res-item {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -ms-flex-pack: distribute;
  justify-content: space-around;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center
}

#all-info #left .item-1 .result .res-box p {
  margin-top: 13px
}

#all-info #left .item-2 {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column
}


#all-info #left .item-2 .i2-top {
  padding-bottom: 30px;
}

#all-info #left .item-2 .i2 {
  width: 100%;
  margin: 20px auto;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  -ms-flex-pack: distribute;
  justify-content: space-around;
}

#all-info #left .item-2 .i2 .box {
  width: 30%;
  height: 67px;
  margin-bottom: 20px;
  padding: 20px auto;
  background-image: url('/kuang5.png');
  background-size: 100%;
  background-repeat: no-repeat;
}

#all-info #left .item-2 .i2 .box>.num,
#all-info #left .item-2 .i2 .box>.title {
  font-family: PingFangSC-Semibold, PingFang SC;
  font-weight: 600;
  color: #fff;
  text-align: center;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin: 0 auto;
}

#all-info #left .item-2 .i2 .box>.num {
  width: 77px;
  height: 45px;
  font-size: 27px;
  line-height: 45px;
}

#all-info #right {
  width: 73%;
  height: 100%;
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

