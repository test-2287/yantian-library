<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'
import BorrowBubble from '@/components/BorrowBubble.vue'

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

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

const libBorrowArray = [
    { libname: "沙头角街道图书馆", borrowCount: 128 },
    { libname: "中英街道图书馆", borrowCount: 128 },
    { libname: "邂逅图书馆", borrowCount: 128 },
    { libname: "海山街道图书馆", borrowCount: 128 },
    { libname: "盐田图书馆", borrowCount: 128 },
    { libname: "灯塔图书馆", borrowCount: 128 },
    { libname: "悦海图书馆", borrowCount: 128 },
    { libname: "听海图书馆", borrowCount: 128 },
]

</script>

<template>
    <div class="today-borrow-page">
        <div class="title-section">
            <div class="title">今日盐田</div>
            <div class="subtitle">到馆借书</div>
        </div>
        <div class="map-section">
            <YanTianMap />

            <BorrowBubble v-bind="{ libname: '盐田图书馆', username: '李**', position: { x: 318, y: 836 } }" />
            <BorrowBubble v-bind="{ libname: '遇见图书馆', username: '李**', position: { x: 608, y: 578 } }" />
            <BorrowBubble v-bind="{ libname: '梅沙街道图书馆', username: '李**', position: { x: 1063, y: 571 } }" />

        </div>
        <div class="borrow-data-section">
            <swiper :pagination="true" :modules="[Pagination, Autoplay]">
                <swiper-slide v-for="i in 3" :key="`swiper${i}`">
                    <div class="borrow-data-swiper">
                        <div class="data-item" v-for="borrowData in libBorrowArray" :key="`${borrowData.libname}`">
                            <div class="lib-name">{{ borrowData.libname }}</div>
                            <div class="borrow-count">{{ borrowData.borrowCount }} 册</div>
                        </div>
                    </div>
                </swiper-slide>
            </swiper>
        </div>
    </div>
</template>

<style scoped lang="scss">
.today-borrow-page {
    height: 1216px;
    padding: 70px;
    position: relative;
}

.title-section {
    .title {
        font-size: 90px;
        line-height: 130px;
        font-weight: 600;
        color: #3692FF;
    }

    .subtitle {
        font-size: 64px;
        line-height: 93px;
        font-weight: 600;
        color: #3692FF;
    }
}

.borrow-data-section {
    position: absolute;
    width: 856px;
    top: 382px;
    left: 80px;

    .borrow-data-swiper {
        width: 856px;
        height: 650px;
        border: 4px solid #3692FF;
        border-radius: 40px;
        padding: 49px;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;

        .data-item {
            width: 350px;
            height: 117px;
            padding-left: 40px;
            padding-bottom: 18px;
            border-bottom: 3px solid #3692FF;

            font-size: 32px;
            line-height: 46px;
            color: #3692FF;
            font-weight: 700 !important;

            &:nth-child(2n+1) {
                margin-right: 50px;
            }

            &:not(:nth-last-child(-n+2)) {
                margin-bottom: 30px;
            }

        }
    }
}

.map-section {
    position: absolute;
    top: 100px;
    left: 1091px;
}

::v-deep .swiper {
    padding-bottom: 110px;
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