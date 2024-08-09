<script setup>
import FloorDisplay from './components/FloorDisplay.vue';
// import LibTemperature from './components/LibTemperature.vue';
import HalfYearArrive from './components/HalfYearArrive.vue'
import MonthBookStatus from './components/MonthBookStatus.vue'
import MonthBookRank from './components/MonthBookRank.vue'
import TodayVisitor from "./components/TodayVisitor.vue";
import TodayLibCondition from './components/TodayLibCondition.vue'
import TodayBorrow from './components/TodayBorrow.vue'
import TopBorrower from './components/TopBorrower.vue'
import NewUser from './components/NewUser.vue'
import NewFollow from './components/NewFollow.vue'
import BookCirculate from './components/BookCirculate.vue'

import IconTree from '@/assets/svg/tree.svg';
import IconNoticeBubble from '@/assets/svg/bubble-yellow.svg';
import ImageQRCode from '@/assets/svg/index-qrcode.svg';
import ImageEvent from '@/assets/svg/index-event-image.svg';

import { ref, nextTick } from 'vue';
import { eachDayOfInterval, endOfMonth, endOfWeek, format, isSameMonth, isToday, startOfMonth, startOfWeek } from 'date-fns';
import { throttle, debounce } from 'lodash-es';
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';



const animationOrder = [
  FloorDisplay,  //0
  TodayLibCondition, //1
  TodayVisitor, //2
  HalfYearArrive, //3
  TodayBorrow, //4
  MonthBookStatus, //5
  NewUser, //6
  TopBorrower, //7
  NewFollow, //8
  MonthBookRank, //9
  BookCirculate //10
]

const curAnimation = ref(0)

// const today = new Date(2024, 8, 1)
const today = new Date()
const startDate = startOfWeek(startOfMonth(today), { weekStartsOn: 1 })
const endDate = endOfWeek(endOfMonth(today), { weekStartsOn: 1 })
const days = eachDayOfInterval({ start: startDate, end: endDate })
const formatDays = []
days.forEach(day => {
  formatDays.push({
    date: format(day, 'd'),
    isCurrentMonth: isSameMonth(day, today),
    isToday: isToday(day),
    eventNum: 3 
    // hasNewEvent: true // 如果当日有新活动需要加上这个字段
  })
})


formatDays[15].hasNewEvent = true
formatDays[18].hasNewEvent = true


const isLibOpen = ref(true)  // 闭馆为flase

const videoRef = ref(null)
const isPlay = ref(false)
const videoToggle = () => {
  if (!isPlay.value) {
    videoRef.value.play()
    isPlay.value = true
    console.log('play')
  } else {
    videoRef.value.pause()
    isPlay.value = false
    console.log('pause')
  }
}

const playVideo = () => {
  
  console.log('play the video')
  if (curAnimationIndex.value == 0) {
    videoRef.value.currentTime = 0
  }
  videoRef.value.play()
}

const showVideo = ref(false)
const playNext = async () => {

  curAnimation.value = -1

  if (curAnimationIndex.value == 0) {
    showVideo.value = true
  }
  if (curAnimationIndex.value == 9) {
    curAnimation.value = curAnimationIndex.value = 10
    return
  }
  if (curAnimationIndex.value == 10) {
    curAnimation.value = curAnimationIndex.value = 0
    currentPause.value = 0
    showVideo.value = false
    return
  }

  await nextTick();
  playVideo();

}

let curAnimationIndex = ref(0)
let currentPause = ref(0)
const pauseTimeArray = [6.5, 7.5, 13, 14.4, 14.8, 20.5, 25.5, 30, 36]

const checkPause = () => {
  if (currentPause.value <= 8 && videoRef.value.currentTime >= pauseTimeArray[currentPause.value]) {
    videoRef.value.pause()
    console.log(videoRef.value.currentTime)
    currentPause.value += 1
    
    if (curAnimationIndex.value <= 0) {
      curAnimation.value = curAnimationIndex.value = 1

      return
    } else if (curAnimationIndex.value > 0 && curAnimationIndex.value < 9) {
      curAnimationIndex.value += 1
      curAnimation.value = curAnimationIndex.value

      return
    } 
    // else if() {

    // }

  }
}




</script>

<template>

  <div class="homepage">

    <div class="section-event">

      <div class="calendar-section">
        <div class="notes">
          <span class="green">当天有活动进行中</span>
          <span class="orange">当天有新活动开始</span>
        </div>
        
        <div class="title-box">6月活动新日历</div>
        <div class="calendar">
          <div class="calendar-header">
            <div>周一</div>
            <div>周二</div>
            <div>周三</div>
            <div>周四</div>
            <div>周五</div>
            <div>周六</div>
            <div>周日</div>
          </div>
          <div class="calendar-grid" ref="calendarRef">
            <div class="date-box" :class="{ istoday: day.isToday }" v-for="(day, index) in formatDays"
              :key="`day${index}`">
              <template v-if="day.isCurrentMonth"> {{ day.date }} </template>
              <span class="event" :class="{new: day.hasNewEvent}" v-if="day.eventNum && day.isCurrentMonth">{{day.eventNum}}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="week-event">
        <div class="title-box">本周活动</div>
        <Swiper :modules="[Autoplay]">
          <swiper-slide v-for="i in 3" :key="`event${i}`">
            <div class="event-box">
              <div class="left"> 
                <ImageEvent />
                <!-- <img src="@/assets/svg/index-event-image.svg?url" alt=""> -->
              </div>
              <div class="right">
                <div class="event-title">团体招聘 | 探索海洋秘境，预约珊瑚科普之旅</div>
                <div class="event-detail">
                  <div class="detail-item">
                    <div class="item-label">时间</div>
                    <div class="item-content">2024年6月20日 下午4:00</div>
                  </div>
                  <div class="detail-item">
                    <div class="item-label">地点</div>
                    <div class="item-content">盐田区图书馆四楼海洋文化园</div>
                  </div>
                  <div class="detail-item">
                    <div class="item-label">对象</div>
                    <div class="item-content">6岁以上团体（人数限10-20人）</div>
                  </div>
                </div>
              </div>
            </div>
          </swiper-slide>
        </Swiper>
        <div class="qrcode-box">
          <div class="header">读者之星</div>
          <div class="qrcode-image-box">
            <ImageQRCode class="qrcode" @click="videoToggle" />
          </div>
        </div>

      </div>

    </div>

    <div class="section-main">
      <video ref="videoRef" width="2800" height="1216" class="background-video" @timeupdate="checkPause" v-show="showVideo" muted>
        <source src="@/assets/background-animation.mp4">
      </video>

      <component :is="animationOrder[curAnimation]" @current-animation-finish="playNext" v-show="curAnimation != -1" />
    </div>

    <div class="section-notice">

      <!-- <div class="video-test" @click="videoToggle">video toggle</div> -->

      <div class="notice-container">

        <div class="title-box">通知公告</div>

        <template v-if="isLibOpen">
          <swiper :modules="[Pagination, Autoplay]" :pagination="{ type: 'fraction' }">
            <swiper-slide v-for="i in 4" :key="`notice${i}`">
              <div class="notice-box">
                <div class="notice-header">
                  <div class="header-left notice-date-box">
                    <div class="notice-month">12月</div>
                    <div class="notice-date">19</div>
                  </div>
                  <div class="notice-title">栖息图书馆获评2023年度深圳十佳共享艺文空间</div>
                </div>
                <div class="notice-content">
                  栖息图书馆是深圳市盐田区图书馆是“海书房”之一，占地281.1㎡。外观造型以传统欧式风格奠定基调，融合现代简约风格，以白色为主色调，整体营造了“圣洁、高雅、开放、通透”的文化殿堂氛围。
                  <br>
                  洁白的纱幔搭配大落地窗，在阳光的照耀下，整个图书馆都显得高雅了起来。
                  <br>
                  栖息图书馆是深圳市盐田区图书馆是“海书房”之一，占地281.1㎡。外观造型以传统欧式风格奠定基调，融合现代简约风格，以白色为主色调，整体营造了“圣洁、高雅、开放、通透”的文化殿堂氛围。
                </div>
              </div>
            </swiper-slide>
          </swiper>
        </template>
        <template v-else>
          <swiper :modules="[Pagination, Autoplay]" :pagination="{ type: 'fraction' }">
            <swiper-slide v-for="i in 4" :key="`close${i}`">
              <div class="closed-box">
                <div class="lib-list">
                  <div class="lib-item" v-for="i in 5" :key="`lib${i}`">
                    <div class="lib-name">中英街图书馆</div>
                    <div class="lib-status">今日闭馆</div>
                  </div>
                </div>
              </div>
            </swiper-slide>
          </swiper>
        </template>

        <div class="icon-trees-box">
          <IconTree class="icon-tree" />
          <IconTree class="icon-tree" />
          <IconTree class="icon-tree" />
        </div>
        <IconNoticeBubble class="icon-bubble" />

      </div>

    </div>
  </div>
</template>

<style scoped lang="scss">
.homepage {
  width: 4864px;
  height: 1216px;
  display: grid;
  grid-template-columns: 1032px 1fr 1032px;
}

.section-event,
.section-notice {
  width: 1032px;
  height: 1216px;
  background-color: #C0DDFF;
}

.section-main {
  width: 2800px;
  height: 1216px;
  position: relative;
}

.background-video {
  position: absolute;
  /* width: 2828px; */
  height: 1216px;
  object-fit: cover;
  z-index: -1;
  left: 0;
  top: 0
}

.section-event {
  /* padding: 130px 60px 91px; */
  padding: 0 60px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.calendar-section {
  position: relative;
  background-color: #fff;
  border: 4px solid #3692FF;
  border-radius: 30px;
  width: 888px;
  /* height: 564px; */
  margin-top: 50px;

  .notes,
  .title-box {
    position: absolute
  }

  .notes {
    top: -50px;
    right: 0;
    font-size: 24px;
    line-height: 34.75px;
    color: #3692FF;
    display: flex;
    align-items: center;
    > span {
      display: flex;
      align-items: center;
      margin-left: 10px;
      font-weight: 600;
      &::before {
        content: '';
        width: 24px;
        height: 24px;
        border-radius: 50%;
        margin-right: 10px;
      }
      &.green::before {
        background-color: #68C945;
      }
      &.orange::before {
        background-color: #FF852D
      }
    }
  }

  .title-box {
    left: 30px;
    top: -60px;
    width: 350px;
    height: 100px;
    border: 4px solid #3692FF;
    border-radius: 50px;
    box-shadow: -14px -14px #3692FF;
    background-color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 48px;
    line-height: 56px;
    color: #3692FF;

  }

  .calendar {
    padding: 56px 40px;

    .calendar-header {
      margin-bottom: 25px;
      display: flex;
      justify-content: space-around;
      font-size: 24px;
      line-height: 35px;
      color: #88BFFF;
    }
  }

  .calendar-grid {
    width: 808px;
    /* height: 410px; */
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-gap: 20px;

    .date-box {
      position: relative;
      width: 100px;
      height: 70px;
      background-color: #E7F2FF;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 32px;
      line-height: 48px;
      color: #3692FF;
      font-weight: 600;

      &.istoday {
        background-color: #88BFFF;
        color: #fff;
      }

      .event {
        position: absolute;
        top: -10px;
        left: -9px;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background-color: #68C945;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        font-size: 20px;
        line-height: 29px;
        &.new {
          background-color: #FF852D;
        }
      }
    }
  }
}

.week-event {
  width: 888px;
  height: 327px;
  border: 4px solid #3692FF;
  border-radius: 30px;
  /* margin-top: 94px; */
  padding: 44px 30px;
  background-color: #fff;
  position: relative;



  .title-box {
    position: absolute;
    width: 270px;
    height: 60px;
    background-color: #fff;
    border-radius: 30px;
    border: 3px solid #3692FF;
    top: -30px;
    left: calc(50% - 135px);
    display: flex;
    justify-content: center;
    align-items: center;
    color: #88BFFF;
    font-size: 32px;
    line-height: 46px;
  }

  .event-box {
    display: flex;
  }

  .left {
    flex-shrink: 0;
    max-width: 340px;
    height: 250px;
    border-radius: 20px;
    margin-right: 25px;

    > img {
      max-width: 340px;
      max-height: 250px;
    }

  }

  .right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    .event-title {
      font-size: 32px;
      font-weight: 700;
      line-height: 46.34px;
      color: #3692FF;
    }

    .event-detail {
      .detail-item:not(:last-child) {
        margin-bottom: 10px;
      }

      .detail-item {
        display: flex;
        font-size: 20px;
        font-weight: 500;
        line-height: 28.96px;

        .item-label {
          color: #8A8A8A;
          margin-right: 10px;
        }

        .item-content {
          color: #000;
        }
      }
    }

  }

  .qrcode-box {
    position: absolute;
    z-index: 1;
    right: -30px;
    bottom: -30px;
    width: 140px;
    height: 183px;
    border: 4px solid #3692FF;
    border-radius: 20px;
    background-color: #fff;
    /* padding: 20px; */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .header {
      font-size: 24px;
      font-weight: 500;
      line-height: 34.75px;
      color: #3692FF;
      text-align: center;
      margin-bottom: 8px;
    }

    .qrcode-image-box {
      width: 120px;
      height: 120px;
    }
  }


}


.section-notice {
  padding: 0 66px;
  display: flex;
  align-items: center;
}

.notice-container {
  width: 900px;
  height: 970px;
  border: 4px solid #3692FF;
  border-radius: 40px;
  background-color: #fff;
  position: relative;

  .title-box {
    position: absolute;
    top: -50px;
    right: 64px;
    background-color: #fff;
    width: 290px;
    height: 100px;
    border-radius: 60px;
    border: 4px solid #3692FF;
    box-shadow: 15px -15px #3692FF;
    /* font-family: Alimama FangYuanTi VF; */
    font-size: 48px;
    font-weight: 500;
    line-height: 57.6px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #3692FF;

  }

  .notice-box {
    width: 100%;
    height: 100%;
    padding: 127px 49px 163px;

    .notice-header {
      display: flex;
      align-items: center;
      padding-bottom: 46px;
      border-bottom: 3px solid #3692FF;
    }

    .notice-date-box {
      width: 130px;
      height: 143px;
      border: 3px solid #3692FF;
      border-radius: 20px;
      overflow: hidden;
      margin-right: 47px;
      flex-shrink: 0;

      .notice-month {
        height: 52px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 24px;
        font-weight: 500;
        line-height: 34.75px;
        color: #3692FF;
        border-bottom: 3px solid #3692FF;
        background-color: #E7F2FF;
      }

      .notice-date {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 64px;
        font-weight: 500;
        line-height: 87.42px;
        color: #3692FF;
      }
    }

    .notice-title {
      font-size: 40px;
      font-weight: 700;
      line-height: 57.92px;
      color: #3692FF;
    }

    .notice-content {
      padding-top: 54px;
      font-size: 30px;
      font-weight: 500;
      line-height: 43.44px;
      color: #3692FF;

    }

  }

  .closed-box {
    padding: 125px 45px 120px;

    .lib-item {
      height: 120px;
      width: 807px;
      border-radius: 20px;
      background-color: #E7F2FF;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 39px;

      &:not(:last-child) {
        margin-bottom: 30px;
      }

      .lib-name {
        font-size: 40px;
        font-weight: 700;
        line-height: 57.92px;
        color: #3692FF;
      }

      .lib-status {
        font-size: 36px;
        font-weight: 700;
        line-height: 52.13px;
        color: #FF852D;
      }

    }
  }

  .icon-trees-box {
    position: absolute;
    bottom: -65px;
    left: 45px;
  }

  .icon-tree {
    margin-right: -20px;
    width: 79px;
    height: 129px;
  }

  .icon-bubble {
    position: absolute;
    left: 61px;
    top: -80px;
  }

  :deep(.swiper-pagination-fraction) {
    font-size: 36px;
    line-height: 49.18px;
    color: #3692FF;
    position: absolute;
    width: 90px;
    right: 49px;
    bottom: 42px;
    left: unset;
  }

  :deep(.swiper-pagination-current) {
    font-weight: 700;
  }

  :deep(.swiper-pagination-total) {
    font-weight: 700;
  }

}
</style>
