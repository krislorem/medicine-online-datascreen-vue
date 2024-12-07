<template>
  <div class="home">
    <nav>
      <h1>中医在线考核可视化大屏</h1>
    </nav>
    <div id="mid-bar">
      <select id="info">
        <option>0515-test</option>
      </select>
    </div>
    <div id="all-info">
      <div id="left">
        <div class="item item-1">
          <p class="top-name"><span>考核信息</span></p>
          <p class="time-title"><span>{{ quizItem?.isOver ? '考核已开始' : '考核已结束' }}</span></p>
          <div class="time-container">
            <div class="time-box" style=";"><span class="time-num">{{ quizItem?.isOver ? '考核已开始' : '' }}</span></div>
            <div class="time-box" style=";"><span class="time-num">天</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ }}</span></div>
            <div class="time-box" style=";"><span class="time-num">时</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ }}</span></div>
            <div class="time-box" style=";"><span class="time-num">分</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ }}</span></div>
            <div class="time-box" style=";"><span class="time-num">秒</span></div>
          </div>
          <div class="result">
            <div class="ivu-carousel" style="height: 100%;">
              <button @click="prevSlide" type="button" class="left ivu-carousel-arrow ivu-carousel-arrow-hover">
                <i class="ivu-icon ivu-icon-ios-arrow-back"></i>
              </button>
              <div class="ivu-carousel-list">
                <div class="ivu-carousel-track higher" :style="sliderStyles"
                  style="transition: transform 500ms;visibility: visible">
                  <div class="ivu-carousel-item" v-for="paper in quizPaper" :key="paper.title" :style="sliferItemStyles">
                    <div class="res-topbar">
                      <span>{{ paper.title }}</span>
                      <span>{{ paper.totalQuestion }}题/{{ paper.totalScore }}分</span>
                    </div>
                    <div class="res-box">
                      <div class="res-item">
                        <span>单选</span>
                        <p>{{ paper.simpleScore }}题/{{ paper.singleScore }}分</p>
                      </div>
                      <div class="res-item">
                        <span>多选</span>
                        <p>{{ paper.multipleScore }}题/{{ paper.singleScore }}分</p>
                      </div>
                      <div class="res-item">
                        <span>简答</span>
                        <p>{{ paper.blankScore }}题/{{ paper.singleScore }}分</p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <button @click="nextSlide" type="button" class="right ivu-carousel-arrow ivu-carousel-arrow-hover">
                <i class="ivu-icon ivu-icon-ios-arrow-forward"></i>
              </button>
              <ul class="ivu-carousel-dots ivu-carousel-dots-none">
                <li class="ivu-carousel-active">
                  <button type="button" class></button>
                </li>
              </ul>
            </div>

          </div>
        </div>
        <div class="item item-2">
          <p class="top-name i2-top"><span>学员信息</span></p>
          <div class="i2">
            <div class="box">
              <p class="num bg-lg-blue">{{ quizStudent?.ought }}</p>
              <p class="title bg-lg-blue">应考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">{{ quizStudent?.in }}</p>
              <p class="title bg-lg-cyan">签到人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">{{ quizStudent?.actual }}</p>
              <p class="title bg-lg-red">实考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue">{{ quizStudent?.alloc }}</p>
              <p class="title bg-lg-blue">分配试卷</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">{{ quizStudent?.answering }}</p>
              <p class="title bg-lg-cyan">答题中</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">{{ quizStudent?.finished }}</p>
              <p class="title bg-lg-red">完成考试</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue2">{{ quizStudent?.nin }}</p>
              <p class="title bg-lg-blue2">未签到</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan2">{{ quizStudent?.absent }}</p>
              <p class="title bg-lg-cyan2">未考核</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red2">{{ quizStudent?.passed }}</p>
              <p class="title bg-lg-red2">合格人数</p>
            </div>
          </div>
        </div>
      </div>
      <div id="right">
        <div class="item mb-22">
          <!-- echarts -->
          <div style="width: 100%;height: 335px;">
            <div id="msg1"
              style="width: 100%; height: 335px; -webkit-tap-highlight-color: transparent; user-select: none; position: relative;">
            </div>
          </div>
        </div>
        <div class="item">
          <div style="width: 100%; height: 335px;">
            <div id="msg2"
              style="width: 100%; height: 335px; -webkit-tap-highlight-color: transparent; user-select: none; position: relative;">
            </div>
          </div>
        </div>
      </div>
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
  margin: 48px auto 0;
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
  margin-top: -15px;
}

#all-info {
  width: 100%;
  height: 796px;
  margin: 20px auto 10px;
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
  height: 40%;
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

#all-info #left .item-2 .i2 .box>.num {
  width: 77px;
  height: 45px;
  font-size: 27px;
  line-height: 45px
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

#all-info #left .item-2 .i2 .box>.title {
  width: 64px;
  height: 22px;
  font-size: 15px;
  line-height: 22px
}

.ivu-carousel {
  position: relative;
  display: block;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -ms-touch-action: pan-y;
  touch-action: pan-y;
  -webkit-tap-highlight-color: transparent
}

.ivu-carousel-list,
.ivu-carousel-track {
  -webkit-transform: translateZ(0);
  transform: translateZ(0)
}

.ivu-carousel-list {
  margin: 0;
  padding: 0
}

.ivu-carousel-list,
.ivu-carousel-track {
  position: relative;
  display: block;
  overflow: hidden
}

.ivu-carousel-track {
  top: 100%;
  left: 0;
  z-index: 1
}

.ivu-carousel-track.higher {
  z-index: 2;
  top: 0;
}

.ivu-carousel-item {
  float: left;
  height: 100%;
  min-height: 1px;
  display: block
}

.ivu-carousel-arrow {
  border: none;
  outline: none;
  padding: 0;
  margin: 0;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  cursor: pointer;
  display: none;
  position: absolute;
  top: 50%;
  z-index: 10;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
  -webkit-transition: .2s;
  transition: .2s;
  background-color: rgba(31, 45, 61, .11);
  color: #fff;
  text-align: center;
  font-size: 1em;
  font-family: inherit;
  line-height: inherit
}

.ivu-carousel-arrow:hover {
  background-color: rgba(31, 45, 61, .5)
}

.ivu-carousel-arrow>* {
  vertical-align: baseline
}

.ivu-carousel-arrow.left {
  left: 16px
}

.ivu-carousel-arrow.right {
  right: 16px
}

.ivu-carousel-arrow-always {
  display: inherit
}

.ivu-carousel-arrow-hover {
  display: inherit;
  opacity: 0
}

.ivu-icon {
  display: inline-block;
  font-family: Ionicons;
  -webkit-speak: none;
  /* 防止元素被屏幕阅读器朗读 */
  font-style: normal;
  font-weight: 400;
  font-variant: normal;
  text-transform: none;
  text-rendering: auto;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  vertical-align: middle
}

.ivu-icon-ios-arrow-back:before {
  content: "‹"
}

.ivu-icon-ios-arrow-forward:before {
  content: "›"
}

.ivu-carousel:hover .ivu-carousel-arrow-hover {
  opacity: 1
}

.ivu-carousel-dots {
  z-index: 10;
  display: none;
  position: relative;
  list-style: none;
  text-align: center;
  padding: 0;
  width: 100%;
  height: 17px
}

.ivu-carousel-dots-inside {
  display: block;
  position: absolute;
  bottom: 3px
}

.ivu-carousel-dots-outside {
  display: block;
  margin-top: 3px
}

.ivu-carousel-dots li {
  position: relative;
  display: inline-block;
  vertical-align: top;
  text-align: center;
  margin: 0 2px;
  padding: 7px 0;
  cursor: pointer
}

.ivu-carousel-dots li button {
  border: 0;
  cursor: pointer;
  background: #8391a5;
  opacity: .3;
  display: block;
  width: 16px;
  height: 3px;
  border-radius: 1px;
  outline: none;
  font-size: 0;
  color: transparent;
  -webkit-transition: all .5s;
  transition: all .5s
}

.ivu-carousel-dots li button.radius {
  width: 6px;
  height: 6px;
  border-radius: 50%
}

.ivu-carousel-dots li:hover>button {
  opacity: .7
}

.ivu-carousel-dots li.ivu-carousel-active>button {
  opacity: 1;
  width: 24px
}

.ivu-carousel-dots li.ivu-carousel-active>button.radius {
  width: 6px
}

#all-info #right {
  width: 73%;
  height: 100%;
}

#all-info #right .item {
  width: 100%;
  height: 338px;
  margin-left: 5px;
  background-image: url(/kuang1.png);
  background-size: 100% 100%
}

#all-info #right .mb-22 {
  margin-bottom: 19px
}

.bg-lg-blue {
  background: -webkit-gradient(linear, left top, left bottom, from(#8ac4ff), to(#5999f4));
  background: linear-gradient(180deg, #8ac4ff, #5999f4)
}

.bg-lg-cyan {
  background: -webkit-gradient(linear, left top, left bottom, from(#92eef2), to(#62e4eb));
  background: linear-gradient(180deg, #92eef2, #62e4eb)
}

.bg-lg-red {
  background: -webkit-gradient(linear, left top, left bottom, from(#ee3f47), to(#9a1b35));
  background: linear-gradient(180deg, #ee3f47, #9a1b35)
}

.bg-lg-blue2 {
  background: -webkit-gradient(linear, left top, left bottom, from(#4d7ed5), to(#0a47b3));
  background: linear-gradient(180deg, #4d7ed5, #0a47b3)
}

.bg-lg-cyan2 {
  background: -webkit-gradient(linear, left top, left bottom, from(#3bd3d6), to(#158c98));
  background: linear-gradient(180deg, #3bd3d6, #158c98)
}

.bg-lg-red2 {
  background: -webkit-gradient(linear, left top, left bottom, from(#d7606b), to(#a72f4d));
  background: linear-gradient(180deg, #d7606b, #a72f4d)
}
</style>
<script setup lang="ts">
import * as echarts from 'echarts';
import { ref, computed, onMounted, onUnmounted } from 'vue'
import axios from 'axios';
interface DataRes {
  /*编码 0表示成功，其他值表示失败 */
  code: number;

  /*消息内容 */
  msg: string;

  /*响应数据 */
  data: {
    /*考核名称 */
    titles: Record<string, unknown>[];

    /* */
    quizCity: {
      /*城市名称 */
      cities: Record<string, unknown>[];

      /*应考人数 */
      ought: Record<string, unknown>[];

      /*实考人数 */
      actual: Record<string, unknown>[];

      /*完成考核 */
      finished: Record<string, unknown>[];

      /*合格人数 */
      passed: Record<string, unknown>[];

      /*不合格人数 */
      failed: Record<string, unknown>[];

      /*未考人数 */
      absent: Record<string, unknown>[];
    };

    /* */
    quizItem: {
      /*是否结束 */
      isOver: number;

      /*结束日期 */
      endTime: string;

      /*考卷信息结果集 */
      quizPaper: {
        /*考卷名称 */
        title: string;

        /*单选题数 */
        simpleScore: number;

        /*多选题数 */
        multipleScore: number;

        /*填空题数 */
        blankScore: number;

        /*每题分值(上三种题型数相加即为总题数，对应乘分值相加即为总分值) */
        singleScore: number;

        /*总提数 */
        totalQuestion: number;

        /*总分 */
        totalScore: number;
      }[];
    };

    /* */
    quizStudent: {
      /*总应考人数 */
      ought: number;

      /*分配试卷 */
      alloc: number;

      /*未签到 */
      nin: number;

      /*签到人数 */
      in: number;

      /*答题中 */
      answering: number;

      /*未考核 */
      absent: number;

      /*实考人数 */
      actual: number;

      /*总完成考试 */
      finished: number;

      /*总合格人数 */
      passed: number;
    };
  }[];
}

const request = axios.create({
  baseURL: 'https://localhost:8080/quiz/data', // 替换为您的 API 基础 URL
});
const currentSlide = ref(0);
const quizData = ref<DataRes['data'][0] | null>(null);
const quizTitle = quizData.value?.titles;
//地区考核信息结果集
const quizCity = quizData.value?.quizCity;
//考核信息结果集
const quizItem = quizData.value?.quizItem;
const endDate = new Date(quizItem!.endTime)
//考核分卷信息结果集
const quizPaper = quizItem?.quizPaper
//学员信息结果集
const quizStudent = quizData.value?.quizStudent;
const labelOption = {
  show: true,
  position: 'insideBottom',
  distance: 15,
  align: 'left',
  verticalAlign: 'middle',
  rotate: 90,
  formatter: '{c}  {name|{a}}',
  fontSize: 12,
  rich: {
    name: {}
  }
};
const option1 = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'shadow'
    }
  },
  legend: {
    left: 'right',
    textStyle: {
      color: '#fff',
    },
    data: ['应考人数', '实考人数', '完成考核']
  },
  xAxis: [
    {
      type: 'category',
      axisTick: { show: false },
      data: `${quizCity?.cities}`
    }
  ],
  yAxis: [
    {
      type: 'value'
    }
  ],
  series: [
    {
      name: '应考人数',
      type: 'bar',
      barGap: 0,
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.ought}`
    },
    {
      name: '实考人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.actual}`
    },
    {
      name: '完成考核',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.finished}`
    }
  ]
};
const option2 = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'shadow'
    }
  },
  legend: {
    left: 'right',
    textStyle: {
      color: '#fff',
    },
    data: ['合格人数', '不合格人数', '未考人数']
  },
  xAxis: [
    {
      type: 'category',
      axisTick: { show: false },
      data: `${quizCity?.cities}`
    }
  ],
  yAxis: [
    {
      type: 'value'
    }
  ],
  series: [
    {
      name: '合格人数',
      type: 'bar',
      barGap: 0,
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.passed}`
    },
    {
      name: '不合格人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.failed}`
    },
    {
      name: '未考人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: `${quizCity?.absent}`
    }
  ]
};


const sliderStyles = computed(() => {
  return {
    width: `${quizPaper!.length * 100}%`,
    transform: `translate3d(-${currentSlide.value * 100 / quizPaper!.length}%, 0px, 0px)`,
  }
})
const sliferItemStyles = computed(() => {
  return {
    width: `${100 / quizPaper!.length}%`,
    height: 'auto',
    left: '0px'
  }
})
const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % quizPaper!.length;
};

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + quizPaper!.length) % quizPaper!.length;
};
// 明确指定 intervalId 的类型为 number
let intervalId: number | undefined = undefined;

// 开始自动播放
const startAutoPlay = () => {
  intervalId = setInterval(nextSlide, 2000); // 每3秒切换到下一张幻灯片
};

// 停止自动播放
const stopAutoPlay = () => {
  clearInterval(intervalId);
};
onMounted(() => {
  async () => {
    try {
      const response = await request.post<DataRes>('/quiz/data');
      quizData.value = response.data.data[0];
    } catch (error) {
      // 请求失败，处理错误
      console.error('请求失败:', error);
    }
  };
  startAutoPlay();
  let chartDom1 = document.getElementById('msg1');
  let chartDom2 = document.getElementById('msg2');
  let myChart1 = echarts.init(chartDom1);
  let myChart2 = echarts.init(chartDom2);
  option1 && myChart1.setOption(option1);
  option2 && myChart2.setOption(option2);
})
onUnmounted(() => {
  stopAutoPlay();
});
</script>

