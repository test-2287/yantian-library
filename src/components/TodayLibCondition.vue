<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'
import LibConditionBg from '@/assets/svg/lib-condition-bg.svg'
import ConditionBubble from '@/components/ConditionBubble.vue'

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

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

const libConditionArray = [
    { name: "沙头角图书馆", condition: '良好' },
    { name: "中英街图书馆", condition: '良好' },
    { name: "邂逅图书馆", condition: '良好' },
    { name: "盐田图书馆", condition: '良好' },
    { name: "悦海图书馆", condition: '良好' },
    { name: "听海图书馆", condition: '良好' },
]





</script>

<template>
    <div class="today-lib-condition-page">
        <div class="title-section">
            <div class="title">今日盐田</div>
            <div class="subtitle">各馆环境</div>
        </div>
        <div class="weather-section">
            <div class="weather-box">
                <div class="top-section">
                    <div class="title">盐田区</div>
                    <div class="title">15°C</div>
                    <div class="desc">晴转多云</div>
                </div>
                <div class="bottom-section">
                    <div class="item">
                        <div class="item-label">温湿度</div>
                        <div class="item-desc">34％</div>
                    </div>
                    <div class="item">
                        <div class="item-label">空气质量</div>
                        <div class="item-desc">良好</div>
                    </div>
                </div>
            </div>
            <div class="background">
                <LibConditionBg />
            </div>
        </div>
        <div class="map-section">
            <YanTianMap />

            <ConditionBubble v-bind="{ libName: '沙头角图书馆', humidity: 30, position: { x: 208, y: 863 } }" />
            <ConditionBubble v-bind="{ libName: '遇见图书馆', humidity: 30, position: { x: 608, y: 578 } }" />
            <ConditionBubble v-bind="{ libName: '望海图书馆', humidity: 30, position: { x: 1323, y: 692 } }" />
        </div>
        <div class="lib-swiper-section">
            <swiper :pagination="true" :modules="[Pagination, Autoplay]" :autoplay="{ delay: 2000 }">
                <swiper-slide v-for="i in 3" :key="`swiper${i}`">
                    <div class="lib-swiper-box">
                        <div class="lib-item" v-for="lib in libConditionArray" :key="lib.name">
                            <div class="label">{{ lib.name }}</div>
                            <div class="desc">{{ lib.condition }}</div>
                        </div>
                    </div>
                </swiper-slide>
            </swiper>
        </div>
    </div>
</template>

<style scoped lang="scss">
.today-lib-condition-page {
    height: 1216px;
    padding: 70px;
    position: relative;
}

.title-section {
    .title {
        font-size: 90px;
        line-height: 130px;
        color: #3692FF;
        font-weight: 600;
    }

    .subtitle {
        font-size: 64px;
        line-height: 93px;
        color: #88BFFF;
        font-weight: 600;
    }
}

.weather-section {
    position: absolute;
    top: 345px;
    left: 70px;

    .weather-box {
        width: 280px;
        height: 315px;
        padding: 30px;
        border-radius: 20px;
        border: 3px solid #3692FF;
        background: #fff;

        .top-section {
            padding-bottom: 22px;
            border-bottom: 3px solid #88BFFF;

            .title {
                font-size: 32px;
                line-height: 46px;
                color: #3692FF;
                font-weight: 700;
            }

            .desc {
                font-size: 24px;
                line-height: 35px;
                color: #88BFFF;
                font-weight: 500;
            }
        }

        .bottom-section {
            padding-top: 21px;

            .item {
                display: flex;
                justify-content: space-between;
                align-items: center;
                font-size: 24px;
                line-height: 35px;
                font-weight: 700;
                margin-bottom: 8px;

                .item-label {
                    color: #88BFFF
                }

                .item-desc {
                    color: #3692FF;
                }

            }
        }
    }

    .background {
        z-index: -1;
        position: absolute;
        left: 20px;
        top: 20px;
        width: 280px;
        height: 315px;
    }
}

.map-section {
    position: absolute;
    width: 1404px;
    height: 973px;
    left: 300px;
    top: 124px;
}

.lib-swiper-section {
    position: absolute;
    width: 950px;
    left: 1780px;
    top: 70px;
    display: flex;

    .lib-swiper-box {
        width: 950px;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .lib-item {
        width: 450px;
        height: 108px;
        padding: 30px 40px;
        border: 3px solid #3692FF;
        border-radius: 20px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 32px;
        line-height: 46px;
        font-weight: 700;

        .label {
            color: #3692FF;
        }

        .desc {
            color: #68C945;
        }

        &:not(:nth-last-child(-n+2)) {
            margin-bottom: 40px;
        }

        &:nth-child(2n+1) {
            /* margin-right: 50px; */
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