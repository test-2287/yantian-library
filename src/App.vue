<script setup>
// import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'

import FloorDisplay from './components/FloorDisplay.vue';
import LibTemperature from './components/LibTemperature.vue';
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

import { ref, onMounted, computed } from 'vue';
import { eachDayOfInterval, endOfMonth, endOfWeek, format, isSameMonth, isToday, startOfMonth, startOfWeek } from 'date-fns';
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';

// const animationOrder = {
//   FloorDisplay,
//   LibTemperature,
//   HalfYearArrive,
//   MonthBookStatus,
//   MonthBookRank,
//   TodayVisitor,
//   TodayLibCondition,
//   TodayBorrow,
//   NewUser,
//   NewFollow,
//   BookCirculate,
//   TopBorrower,
// }

// const animationArray = [
//   'FloorDisplay',  //0
//   'TodayLibCondition', //1
//   'TodayVisitor', //2
//   'HalfYearArrive', //3
//   'TodayBorrow', //4
//   'MonthBookStatus', //5
//   'NewUser', //6
//   'TopBorrower', //7
//   'NewFollow', //8
//   'MonthBookRank', //9
//   'BookCirculate' //10
// ]

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
    // hasEvent: true   // 如果当日有活动需要加上这个字段
  })
})


const isLibOpen = ref(true)  // 闭馆为flase

// console.log(animationOrder[curAnimation.value]);

</script>

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView /> -->

  <div class="homepage">

    <div class="section-event">

      <div class="calendar-section">
        <span class="notes">*深色当天有活动</span>
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
            <!-- 如果有活动 -->
            <div class="date-box" :class="{ event: day.hasEvent }" v-for="(day, index) in formatDays"
              :key="`day${index}`">
              <template v-if="day.isCurrentMonth"> {{ day.date }} </template>
              <span class="today" v-if="day.isToday">今</span>
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
            <ImageQRCode class="qrcode" />
          </div>
        </div>

      </div>

    </div>

    <div class="section-main">
      <FloorDisplay />
      <!-- <component :is="animationOrder[animationArray[curAnimation]]" /> -->
      <!-- <component :is="animationOrder[curAnimation]" /> -->
    </div>

    <div class="section-notice">

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

<style scoped>
/* header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
} */

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
  width: 2828px;
  height: 1216px;
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
    font-weight: 500;
    line-height: 34.75px;
    color: #3692FF;
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

      &.event {
        background-color: #88BFFF;
        color: #fff;
      }

      .today {
        position: absolute;
        top: -10px;
        left: -9px;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background-color: #FF852D;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        font-size: 20px;
        line-height: 29px;
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
    width: 340px;
    height: 250px;
    border-radius: 20px;
    margin-right: 25px;

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
