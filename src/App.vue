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
import NewUser from './components/NewUser.vue'
import NewFollow from './components/NewFollow.vue'
import BookCirculate from './components/BookCirculate.vue'
import { ref } from 'vue';

const animationOrder = {
  FloorDisplay,
  LibTemperature,
  HalfYearArrive,
  MonthBookStatus,
  MonthBookRank,
  TodayVisitor,
  TodayLibCondition,
  TodayBorrow,
  NewUser,
  NewFollow,
  BookCirculate
}

const animationArray = [
  'FloorDisplay',
  'LibTemperature',
  'HalfYearArrive',
  'MonthBookStatus',
  'MonthBookRank',
  'TodayVisitor',
  'TodayLibCondition',
  'TodayBorrow',
  'NewUser',
  'NewFollow',
  'BookCirculate'
]

const curAnimation = ref(10)


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
        <span class="notes">*当天有活动</span>
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
          <div class="calendar-grid">

          </div>
        </div>
      </div>
    </div>
    <div class="section-main">
      <!-- <FloorDisplay /> -->
      <component :is="animationOrder[animationArray[curAnimation]]" />
    </div>
    <div class="section-notice"></div>
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
  padding: 130px 60px 91px;
}

.calendar-section {
  position: relative;
  background-color: #fff;
  border: 4px solid #3692FF;
  border-radius: 30px;
  width: 888px;
  height: 564px;

  .notes,
  .title-box {
    position: absolute
  }

  .calendar {
    padding: 56px 40px;

    .calendar-header {
      display: flex;
      justify-content: space-around;
      font-size: 24px;
      line-height: 35px;
      color: #88BFFF;
    }
  }

  .calendar-grid {
    width: 808px;
    height: 410px;
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(5, 1fr);
  }
}
</style>
