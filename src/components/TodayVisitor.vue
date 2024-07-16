<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

import { onMounted } from 'vue';


// insertAjacentHTML createElementNS 
const svg = document.getElementById('mySvg');

// Create a rectangle element with the correct namespace
// const rect = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
// rect.setAttribute('x', '10');
// rect.setAttribute('y', '10');
// rect.setAttribute('width', '30');
// rect.setAttribute('height', '30');
// rect.setAttribute('fill', 'blue');

// // Append the rectangle to the SVG
// svg.appendChild(rect);

// 地图svg 各馆对应坐标
const leftPart = [
    { "x": 208.684, "y": 863.401 }, // 沙头角街道图书馆
    { "x": 228.684, "y": 957.401 }, // 中英街道图书馆
    { "x": 243.684, "y": 935.401 }, // 中英街图书馆
    { "x": 258.684, "y": 912.401 }, // 邂逅图书馆
    { "x": 298.684, "y": 892.401 }, // 海山街道图书馆
    { "x": 318.684, "y": 836.401 }, // 盐田图书馆
    { "x": 338.684, "y": 882.401 }, // 灯塔图书馆
]

const middlePart = [
    { "x": 525.684, "y": 610.401 }, // 盐田街道图书馆
    { "x": 608.684, "y": 578.401 }, // 遇见图书馆
    { "x": 696.684, "y": 630.401 } // 春天海图书馆
]

const rightPart = [
    { "x": 974.684, "y": 718.401 }, // 悦海图书馆
    { "x": 1030.68, "y": 598.401 }, // 栖息图书馆
    { "x": 1036.68, "y": 634.401 }, // 听海图书馆
    { "x": 1063.68, "y": 571.401 }, // 梅沙街道图书馆
    { "x": 1178.68, "y": 644.401 }, // 观海图书馆
    { "x": 1323.68, "y": 692.401 } // 望海图书馆
]

// 热力图 原点半径 大36-红#FB461E 中20-橘#FF852D 小20-淡黄#FFE791
onMounted(() => {
    // const heatMapSvg = document.getElementsByClassName('heatMap')[0]; 
    const heatMapSvg = document.querySelector('.heatMap');
    // console.log(heatMapSvg)
    // console.log(circleString)
    heatMapSvg.insertAdjacentHTML('beforeend', circleString)
})
// const heatMapSvg = document.getElementsByClassName('heatMap')[0];
// const heatMapSvg = document.querySelector('.heatMap');    
const heatRed = '#FB461E'
const heatOrange = '#FF852D'
const heatYellow = '#FFE791'
const bigRadius = 36
const middleRadius = 20
const smallRaidus = 20

// console.log(heatMapSvg)
const circleString = `
    <circle cx="${leftPart[0].x}" cy="${leftPart[0].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${leftPart[1].x}" cy="${leftPart[1].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${leftPart[2].x}" cy="${leftPart[2].y}" r="${middleRadius}" fill="${heatYellow}" />
    <circle cx="${leftPart[3].x}" cy="${leftPart[3].y}" r="${middleRadius}" fill="${heatYellow}" />
    <circle cx="${leftPart[4].x}" cy="${leftPart[4].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${leftPart[5].x}" cy="${leftPart[5].y}" r="${bigRadius}" fill="${heatRed}" />
    <circle cx="${leftPart[6].x}" cy="${leftPart[6].y}" r="${middleRadius}" fill="${heatOrange}" />

    <circle cx="${middlePart[0].x}" cy="${middlePart[0].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${middlePart[1].x}" cy="${middlePart[1].y}" r="${bigRadius}" fill="${heatRed}" />
    <circle cx="${middlePart[2].x}" cy="${middlePart[2].y}" r="${middleRadius}" fill="${heatYellow}" />

    <circle cx="${rightPart[0].x}" cy="${rightPart[0].y}" r="${middleRadius}" fill="${heatYellow}" />
    <circle cx="${rightPart[1].x}" cy="${rightPart[1].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${rightPart[2].x}" cy="${rightPart[2].y}" r="${middleRadius}" fill="${heatYellow}" />
    <circle cx="${rightPart[3].x}" cy="${rightPart[3].y}" r="${middleRadius}" fill="${heatOrange}" />
    <circle cx="${rightPart[4].x}" cy="${rightPart[4].y}" r="${middleRadius}" fill="${heatYellow}" />
    <circle cx="${rightPart[5].x}" cy="${rightPart[5].y}" r="${middleRadius}" fill="${heatOrange}" />



`

/*  */ 

// const tempContainer = document.createElement('div')
// tempContainer.innerHTML = circleString

// heatMapSvg.insertAdjacentHTML('beforeend', circleString)


const visitorArray = [
    {
        libname: "盐田图书馆",
        count: 1049
    },
    {
        libname: "悦海图书馆",
        count: 1049
    },
    {
        libname: "听海图书馆",
        count: 1049
    },
    {
        libname: "灯塔图书馆",
        count: 1049
    },
]

</script>

<template>
    <div class="today-visitor-page">
        <div class="title-section">
            <div class="title">今日盐田</div>
            <div class="subtitle">到馆人数</div>
        </div>
        <div class="map-section">
            <YanTianMap class="heatMap" />
        </div>
        <div class="visitor-data-section">
            <Swiper :pagination="true" :modules="[Pagination, Autoplay]">
                <swiper-slide v-for="i in 3" :key="`swiper${i}`">
                    <div class="data-box">
                        <div class="data-item" v-for="visitorData in visitorArray" :key="visitorData.libname">
                            <div class="lib-name">{{ visitorData.libname }}</div>
                            <div class="visitor-number">{{ visitorData.count }}人</div>
                            <div class="status-dot"></div>
                        </div>
                    </div>
                </swiper-slide>
            </Swiper>
        </div>
    </div>
</template>

<style scoped lang="scss">
.today-visitor-page {
    height: 1216px;
    padding: 70px;
    position: relative;
}

.title-section {
    position: absolute;
    top: 70px;
    left: 70px;

    .title {
        font-size: 90px;
        line-height: 130px;
        color: #3692FF;
        font-weight: 600;
    }

    .subtitle {
        font-size: 64px;
        line-height: 92px;
        color: #88BFFF;
        font-weight: 600;
    }
}

.map-section {
    position: absolute;
    top: 124px;
    left: 300px;
}

.visitor-data-section {
    position: absolute;
    top: 70px;
    right: 100px;
    width: 850px;

    .data-box {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;

        .data-item {
            width: 400px;
            height: 180px;
            flex-shrink: 0;
            border-radius: 30px;
            border: 3px solid #3692FF;
            margin-bottom: 40px;
            padding: 27px 37px;
            position: relative;

            &:nth-last-child(-n+2) {
                margin-bottom: 0
            }

            .lib-name {
                font-size: 32px;
                line-height: 46px;
                color: #88BFFF;
                font-weight: 700;
            }

            .visitor-number {
                font-size: 60px;
                line-height: 87px;
                color: #3692FF;
                font-weight: 700;
            }

            .status-dot {
                width: 40px;
                height: 40px;
                border-radius: 50%;
                position: absolute;
                top: 30px;
                right: 30px;
                background-color: #FFE791;
            }

        }
    }
}

::v-deep .swiper {
    padding-bottom: 80px;
}

::v-deep .swiper-pagination {
    .swiper-pagination-bullet {
        width: 36px;
        height: 36px;
        background-color: #fff;
        border: 4px solid #3692FF;
        margin: 0 10px;
    }

    .swiper-pagination-bullet-active {
        background-color: #3692FF;
    }
}
</style>