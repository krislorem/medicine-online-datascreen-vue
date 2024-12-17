<template>
  <div class="home">
    <nav>
      <h1>中医在线考核可视化大屏</h1>
    </nav>
    <div id="mid-bar">
      <select id="info" v-model="selectedExamName">
        <option v-for="(exam, index) in examGroups" :key="index" :value="exam.name">
          {{ exam.name }}
        </option>
      </select>
    </div>
    <div id="all-info">
      <div id="left">
        <div class="item item-1">
          <p class="top-name"><span>考核信息</span></p>
          <p class="time-title"><span>{{ selectedExam?.start && (new Date(selectedExam.end) > new Date()) ?
            '考核已开始' : '考核已结束' }}</span></p>
          <div v-if="selectedExam?.start && (new Date(selectedExam.end) > new Date())" class="time-container">
            <div class="time-box" style=";"><span class="time-num">{{ countdown.days }}</span></div>
            <div class="time-box" style=";"><span class="time-num">天</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ countdown.hours }}</span></div>
            <div class="time-box" style=";"><span class="time-num">时</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ countdown.minutes }}</span></div>
            <div class="time-box" style=";"><span class="time-num">分</span></div>
            <div class="time-box" style=";"><span class="time-num">{{ countdown.seconds }}</span></div>
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
                  <div class="ivu-carousel-item" v-for="item in selectedExam?.paperInfoList" :style="sliferItemStyles">
                    <div class="res-topbar">
                      <span>{{ item.paper }}</span>
                      <span>{{ item.totalN }}题/{{ item.totalS }}分</span>
                    </div>
                    <div class="res-box">
                      <div class="res-item">
                        <span>单选</span>
                        <p>{{ item.sin }}题/{{ item.sinN }}分</p>
                      </div>
                      <div class="res-item">
                        <span>多选</span>
                        <p>{{ item.mul }}题/{{ item.mulN }}分</p>
                      </div>
                      <div class="res-item">
                        <span>简答</span>
                        <p>{{ item.blank }}题/{{ item.blankN }}分</p>
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
              <p class="num bg-lg-blue">{{ selectedExam?.studentInfo.studentCount }}</p>
              <p class="title bg-lg-blue">应考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">{{ selectedExam!.studentInfo.finishCountMap['0'] +
                selectedExam!.studentInfo.finishCountMap['1'] }}</p>
              <p class="title bg-lg-cyan">签到人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">{{ selectedExam!.studentInfo.finishCountMap['0'] +
                selectedExam!.studentInfo.finishCountMap['1'] }}</p>
              <p class="title bg-lg-red">实考人数</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue">{{ selectedExam!.studentInfo.paperCount }}</p>
              <p class="title bg-lg-blue">分配试卷</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan">{{ selectedExam!.studentInfo.gradeCountMap['1'] }}</p>
              <p class="title bg-lg-cyan">答题中</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red">{{ selectedExam!.studentInfo.finishCountMap['1'] }}</p>
              <p class="title bg-lg-red">完成考试</p>
            </div>
            <div class="box">
              <p class="num bg-lg-blue2">{{ selectedExam!.studentInfo.studentCount -
                selectedExam!.studentInfo.finishCountMap['0'] + selectedExam!.studentInfo.finishCountMap['1'] }}</p>
              <p class="title bg-lg-blue2">未签到</p>
            </div>
            <div class="box">
              <p class="num bg-lg-cyan2">{{ selectedExam!.studentInfo.studentCount -
                selectedExam!.studentInfo.finishCountMap['0'] + selectedExam!.studentInfo.finishCountMap['1'] }}</p>
              <p class="title bg-lg-cyan2">未考核</p>
            </div>
            <div class="box">
              <p class="num bg-lg-red2">{{ selectedExam!.studentInfo.gradeCountMap['3'] }}</p>
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
import { ref, watch, nextTick, computed, onMounted, onUnmounted } from 'vue'
import axios from 'axios';
interface Data {
  /*考试标题 */
  name: string;

  /*是否开始 */
  start: number;

  /*结束时间 */
  end: string;

  /*考卷信息列表 */
  paperInfoList: {
    /*考卷名 */
    paper: string;

    /*单选分值 */
    sin: number;

    /*多选分值 */
    mul: number;

    /*填空分值 */
    blank: number;

    /*单选数 */
    sinN: number;

    /*多选数 */
    mulN: number;

    /*填空数 */
    blankN: number;

    /*总题数 */
    totalN: number;

    /*总分 */
    totalS: number;
  }[];
  /* 学员信息 */
  studentInfo: {
    /*学员数量 */
    studentCount: number;

    /*考卷数量 */
    paperCount: number;

    /*是否完成数量映射 */
    finishCountMap: Record<string, number>;

    /*学员成绩数量映射 */
    gradeCountMap: Record<string, number>;
  };

  /*地区信息列表 */
  regionInfoList: {
    /*地区名称 */
    city: string;

    /*学员数量 */
    studentCount: number;

    /*是否完成数量映射 */
    finishCountMap: Record<string, number>;

    /*学员成绩数量映射 */
    gradeCountMap: Record<string, number>;
  }[];
};

// 创建一个响应式变量来存储数据
const examGroups = ref<Data[]>(
  [
    {
      "name": "202级专题冬季考试",
      "start": 1,
      "end": "2025-11-01T00:00:00",
      "paperInfoList": [
        {
          "paper": "B卷",
          "sin": 1,
          "mul": 2,
          "blank": 3,
          "sinN": 1,
          "mulN": 1,
          "blankN": 1,
          "totalN": 3,
          "totalS": 6
        }
      ],
      "studentInfo": {
        "studentCount": 2243,
        "paperCount": 1,
        "finishCountMap": {
          "0": 2243,
          "1": 0
        },
        "gradeCountMap": {
          "0": 8,
          "1": 0,
          "2": 96,
          "3": 2139
        }
      },
      "regionInfoList": [
        {
          "city": "宿迁市",
          "studentCount": 351,
          "finishCountMap": {
            "0": 350,
            "1": 0
          },
          "gradeCountMap": {
            "0": 1,
            "1": 0,
            "2": 5,
            "3": 344
          }
        },
        {
          "city": "镇江市",
          "studentCount": 148,
          "finishCountMap": {
            "0": 147,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 3,
            "3": 144
          }
        },
        {
          "city": "无锡市",
          "studentCount": 146,
          "finishCountMap": {
            "0": 145,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 15,
            "3": 130
          }
        },
        {
          "city": "扬州市",
          "studentCount": 151,
          "finishCountMap": {
            "0": 150,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 0,
            "3": 150
          }
        },
        {
          "city": "淮安市",
          "studentCount": 156,
          "finishCountMap": {
            "0": 155,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 0,
            "3": 155
          }
        },
        {
          "city": "常州市",
          "studentCount": 177,
          "finishCountMap": {
            "0": 176,
            "1": 0
          },
          "gradeCountMap": {
            "0": 1,
            "1": 0,
            "2": 6,
            "3": 169
          }
        },
        {
          "city": "南京市",
          "studentCount": 145,
          "finishCountMap": {
            "0": 144,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 21,
            "3": 123
          }
        },
        {
          "city": "南通市",
          "studentCount": 157,
          "finishCountMap": {
            "0": 156,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 30,
            "3": 126
          }
        },
        {
          "city": "苏州市",
          "studentCount": 150,
          "finishCountMap": {
            "0": 149,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 7,
            "3": 142
          }
        },
        {
          "city": "连云港市",
          "studentCount": 207,
          "finishCountMap": {
            "0": 206,
            "1": 0
          },
          "gradeCountMap": {
            "0": 0,
            "1": 0,
            "2": 9,
            "3": 197
          }
        },
        {
          "city": "盐城市",
          "studentCount": 151,
          "finishCountMap": {
            "0": 150,
            "1": 0
          },
          "gradeCountMap": {
            "0": 1,
            "1": 0,
            "2": 0,
            "3": 149
          }
        },
        {
          "city": "徐州市",
          "studentCount": 152,
          "finishCountMap": {
            "0": 151,
            "1": 0
          },
          "gradeCountMap": {
            "0": 3,
            "1": 0,
            "2": 0,
            "3": 148
          }
        },
        {
          "city": "泰州市",
          "studentCount": 165,
          "finishCountMap": {
            "0": 164,
            "1": 0
          },
          "gradeCountMap": {
            "0": 2,
            "1": 0,
            "2": 0,
            "3": 162
          }
        }
      ]
    }
  ]
);

// selectedExamName用于v-model绑定，存储选中的考试名称
const selectedExamName = ref(examGroups.value.length > 0 ? examGroups.value[0].name : '');

// 如果需要根据选中的考试名称获取对应的对象，可以这样操作
const selectedExam = ref(examGroups.value.find(exam => exam.name === selectedExamName.value) || null);
//异步更新
watch(examGroups, (newValue) => {
  // 等待DOM更新
  nextTick(() => {
    // 现在可以安全地访问更新后的DOM
    selectedExamName.value = newValue.length > 0 ? newValue[0].name : ''
    selectedExam.value = newValue.find(exam => exam.name === selectedExamName.value) || null
  });
});
const countdown = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

function updateCountdown() {
  const endTime = new Date(selectedExam!.value!.end).getTime();
  const now = new Date().getTime();
  const diff = endTime - now;

  if (diff < 0) {
    countdown.value = { days: 0, hours: 0, minutes: 0, seconds: 0 };
  } else {
    countdown.value = {
      days: Math.floor(diff / (1000 * 60 * 60 * 24)),
      hours: Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
      minutes: Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)),
      seconds: Math.floor((diff % (1000 * 60)) / 1000),
    };
  }
}

// 立即更新一次倒计时，然后每秒钟更新一次
updateCountdown();
const tIntervalId = setInterval(updateCountdown, 1000);

onUnmounted(() => {
  clearInterval(tIntervalId); // 组件卸载时清除定时器
});
const currentSlide = ref(0);
// 使用 computed 创建一个响应式的 citiesArray
const citiesArray = computed(() => {
  const allCities = new Set(); // 使用 Set 来自动去重
  examGroups.value.forEach(exam => {
    exam.regionInfoList.forEach(region => {
      allCities.add(region.city);
    });
  });
  return Array.from(allCities); // 将 Set 转换为数组
});
// 使用 computed 创建一个响应式的数组，包含所有城市的 studentCount
const allStudentCounts = computed(() => {
  return examGroups.value.flatMap(exam =>
    exam.regionInfoList.map(region => region.studentCount)
  );
});

// 使用 computed 创建两个响应式的数组，分别包含所有 finishCountMap 中键为 '0' 和 '1' 的值
const finishCounts = computed(() => {
  // 初始化两个空数组用于收集 finishCountMap 中键为 '0' 和 '1' 的值
  const countsZero: any[] = [];
  const countsOne: any[] = [];

  examGroups.value.forEach(exam => {
    // 检查 regionInfoList 是否存在
    if (exam.regionInfoList) {
      // 遍历 regionInfoList
      exam.regionInfoList.forEach(region => {
        // 检查 finishCountMap 是否存在
        if (region.finishCountMap) {
          // 添加 finishCountMap 中键为 '0' 的值到 countsZero 数组
          if (region.finishCountMap['0'] !== undefined && region.finishCountMap['0'] !== null) {
            countsZero.push(region.finishCountMap['0']);
          }
          // 添加 finishCountMap 中键为 '1' 的值到 countsOne 数组
          if (region.finishCountMap['1'] !== undefined && region.finishCountMap['1'] !== null) {
            countsOne.push(region.finishCountMap['1']);
          }
        }
      });
    }
  });

  // 返回包含所有 finishCountMap 中键为 '0' 和 '1' 的值的数组
  return { countsZero, countsOne };
});
// 创建一个计算属性，它依赖于两个响应式数组
const sumArray = computed(() => {
  return finishCounts.value.countsOne.map((value, index) => value + finishCounts.value.countsZero[index]);
});
const minusArray = computed(() => {
  return allStudentCounts.value.map((value, index) => value - sumArray.value[index])
})
// 使用 computed 创建四个响应式的数组，分别包含所有 gradeCountMap 中键为 '0', '1', '2', '3' 的值
const gradeCounts = computed(() => {
  // 初始化四个空数组用于收集 gradeCountMap 中特定键的值
  const gradeCounts: any = {
    '0': [],
    '1': [],
    '2': [],
    '3': []
  };

  examGroups.value.forEach(exam => {
    // 检查 regionInfoList 是否存在
    if (exam.regionInfoList) {
      // 遍历 regionInfoList
      exam.regionInfoList.forEach(region => {
        // 检查 gradeCountMap 是否存在
        if (region.gradeCountMap) {
          // 遍历 gradeCountMap 中的特定键
          Object.keys(gradeCounts).forEach(key => {
            if (region.gradeCountMap[key] !== undefined && region.gradeCountMap[key] !== null) {
              // 将 gradeCountMap 中特定键的值添加到对应的数组中
              gradeCounts[key].push(region.gradeCountMap[key]);
            }
          });
        }
      });
    }
  });

  // 返回包含所有 gradeCountMap 中特定键的值的数组
  return gradeCounts;
});
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
      data: citiesArray.value
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
      data: allStudentCounts.value
    },
    {
      name: '实考人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: sumArray.value
    },
    {
      name: '完成考核',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: finishCounts.value.countsOne
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
      data: citiesArray.value
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
      data: gradeCounts.value['3']
    },
    {
      name: '不合格人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: gradeCounts.value['2']
    },
    {
      name: '未考人数',
      type: 'bar',
      label: labelOption,
      emphasis: {
        focus: 'series'
      },
      data: minusArray.value
    }
  ]
};

const wl = computed(() => selectedExam.value!.paperInfoList.length)
const sliderStyles = computed(() => {
  return {
    width: `${wl.value * 100}%`,
    transform: `translate3d(-${currentSlide.value * 100 / wl.value}%, 0px, 0px)`,
  }
})
const sliferItemStyles = computed(() => {
  return {
    width: `${100 / wl.value}%`,
    height: 'auto',
    left: '0px'
  }
})
const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % 2;
};

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + 2) % 2;
};
const intervalId = ref<number | undefined>(0); // 用于存储定时器ID

// 控制自动播放的响应式变量
const shouldAutoPlay = ref(false);
// 开始自动播放
const startAutoPlay = () => {
  intervalId.value = setInterval(nextSlide, 2000); // 每2秒切换到下一张幻灯片
};

// 停止自动播放
const stopAutoPlay = () => {
  clearInterval(intervalId.value);
};

// 监听selectedExam的变化
watch(selectedExam, (newExam) => {
  // 根据paperInfoList的长度决定是否自动播放
  shouldAutoPlay.value = newExam!.paperInfoList.length > 1;
  if (shouldAutoPlay.value) {
    startAutoPlay();
  } else {
    stopAutoPlay();
  }
}, { immediate: true }); // 立即执行以设置初始状态
onMounted(() => {
  const source = axios.CancelToken.source(); // 创建一个取消令牌
  axios.get('http://117.72.48.44:8080/quiz/data', {
    cancelToken: source.token // 传递取消令牌
  }) // 替换为您的API端点
    .then(response => {
      // 将响应数据赋值给examGroups
      examGroups.value = response.data.data;
    })
    .catch(error => {
      console.error('Error fetching data: ', error);
    });
  let chartDom1 = document.getElementById('msg1');
  let chartDom2 = document.getElementById('msg2');
  let myChart1 = echarts.init(chartDom1);
  let myChart2 = echarts.init(chartDom2);
  option1 && myChart1.setOption(option1);
  option2 && myChart2.setOption(option2);
  onUnmounted(() => {
    source.cancel('Component unmounted'); // 组件卸载时取消请求
  });
})
onUnmounted(() => {
  stopAutoPlay();
});
</script>

