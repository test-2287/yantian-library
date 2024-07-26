<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'
import BorrowBubble from '@/components/BorrowBubble.vue'

import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

import { ref, nextTick, onMounted } from 'vue';
import gsap from 'gsap';
import { delay } from 'lodash-es';

// 地图svg 各馆对应坐标
const leftPart = [
    { "x": 208.684, "y": 863.401, libName: '沙头角街道图书馆' }, // 沙头角街道图书馆
    { "x": 228.684, "y": 957.401, libName: '中英街道图书馆' }, // 中英街道图书馆
    { "x": 243.684, "y": 935.401, libName: '中英街图书馆' }, // 中英街图书馆
    { "x": 258.684, "y": 912.401, libName: '邂逅图书馆' }, // 邂逅图书馆
    { "x": 298.684, "y": 892.401, libName: '海山街道图书馆' }, // 海山街道图书馆
    { "x": 318.684, "y": 836.401, libName: '盐田图书馆' }, // 盐田图书馆
    { "x": 338.684, "y": 882.401, libName: '灯塔图书馆' }, // 灯塔图书馆
]

const middlePart = [
    { "x": 525.684, "y": 610.401, libName: '盐田街道图书馆' }, // 盐田街道图书馆
    { "x": 608.684, "y": 578.401, libName: '遇见图书馆' }, // 遇见图书馆
    { "x": 696.684, "y": 630.401, libName: '春天海图书馆' } // 春天海图书馆
]

const rightPart = [
    { "x": 974.684, "y": 718.401, libName: '悦海图书馆' }, // 悦海图书馆
    { "x": 1030.68, "y": 598.401, libName: '栖息图书馆' }, // 栖息图书馆
    { "x": 1036.68, "y": 634.401, libName: '听海图书馆' }, // 听海图书馆
    { "x": 1063.68, "y": 571.401, libName: '梅沙街道图书馆' }, // 梅沙街道图书馆
    { "x": 1178.68, "y": 644.401, libName: '观海图书馆' }, // 观海图书馆
    { "x": 1323.68, "y": 692.401, libName: '望海图书馆' } // 望海图书馆
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

let borrowBubblesArray = ref([])
const getBorrowBubblesArray = () => {
    const leftRandomIndex = Math.floor(Math.random() * leftPart.length)
    const middleRandomIndex = Math.floor(Math.random() * middlePart.length)
    const rightRandomIndex = Math.floor(Math.random() * rightPart.length)

    return [
        {
            username: '李**',
            ...leftPart[leftRandomIndex]
        },
        {
            username: '张**',
            ...middlePart[middleRandomIndex]
        },
        {
            username: '王**',
            ...rightPart[rightRandomIndex]
        }
    ]
}
borrowBubblesArray.value = getBorrowBubblesArray()
const animationBubbles = async () => {
    await nextTick()
    const tlBubble = gsap.timeline({
        onComplete: async () => {
            borrowBubblesArray.value = getBorrowBubblesArray()
            console.log(borrowBubblesArray.value);
            await nextTick()
            animationBubbles()
        }
    });
    tlBubble.from('.borrow-bubble', {
        opacity: 0,
    })
    tlBubble.to('.borrow-bubble', {
        opacity: 1,
        duration: 2,
        stagger: 0.7,
    })
    .to('.borrow-bubble', {
        opacity: 0,
        duration: 2,
        stagger: 0.7,
    })
}

const emit = defineEmits(['current-animation-finish'])

onMounted(() => {
    // animationBubbles()

    setTimeout(() => {
        emit('current-animation-finish')
    }, 4000)
})



</script>

<template>
    <div class="today-borrow-page">
        <div class="title-section">
            <div class="title">今日盐田</div>
            <div class="subtitle">到馆借书</div>
        </div>
        <div class="map-section">
            <YanTianMap />

            <BorrowBubble v-for="borrowItem in borrowBubblesArray" :key="`${borrowItem.username}`" v-bind="borrowItem" />

        </div>
        <div class="borrow-data-section">
            <swiper :pagination="true" :modules="[Pagination, Autoplay]" :autoplay="{ delay: 1000 }">
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
        background-color: #fff;
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

            position: relative;

            &:nth-child(2n+1) {
                margin-right: 50px;
            }

            &:not(:nth-last-child(-n+2)) {
                margin-bottom: 30px;
            }

            &::before {
                content: '';
                display: block;
                position: absolute;
                top: 11px;
                left:0;
                width: 24px;
                height: 24px;
                border-radius: 50%;
                background-color: #FFE791;
                border: 4px solid #3692FF;
            }

        }
    }
}

.map-section {
    position: absolute;
    top: 100px;
    left: 1091px;
}

:deep(.swiper) {
    padding-bottom: 110px;
}

:deep(.swiper-pagination) {
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