<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

import libImage from '@/assets/svg/icon-lib.svg?url'
import { onMounted } from 'vue';

const halfYearMonths = [1, 2, 3, 4, 5, 6]
const libSwiperList = [
    {
        libname: '盐田图书馆',
        borrow: 12394,
        return: 12944,
        image: libImage,
        monthsData: [
            {
                borrow: 200,
                return: 150
            },
            {
                borrow: 220,
                return: 100
            },
            {
                borrow: 100,
                return: 50
            },
            {
                borrow: 200,
                return: 100
            },
            {
                borrow: 220,
                return: 80
            },
            {
                borrow: 80,
                return: 80
            }
        ]
    },
    {
        libname: '邂逅图书馆',
        borrow: 12394,
        return: 12944,
        image: libImage,
        monthsData: [
            {
                borrow: 200,
                return: 150
            },
            {
                borrow: 220,
                return: 100
            },
            {
                borrow: 100,
                return: 50
            },
            {
                borrow: 200,
                return: 100
            },
            {
                borrow: 220,
                return: 80
            },
            {
                borrow: 80,
                return: 80
            }
        ]
    },
    {
        libname: '观海图书馆',
        borrow: 12394,
        return: 12944,
        image: libImage,
        monthsData: [
            {
                borrow: 200,
                return: 150
            },
            {
                borrow: 220,
                return: 100
            },
            {
                borrow: 100,
                return: 50
            },
            {
                borrow: 200,
                return: 100
            },
            {
                borrow: 220,
                return: 80
            },
            {
                borrow: 80,
                return: 80
            }
        ]
    },
    {
        libname: '灯塔图书馆',
        borrow: 12394,
        return: 12944,
        image: libImage,
        monthsData: [
            {
                borrow: 200,
                return: 150
            },
            {
                borrow: 220,
                return: 100
            },
            {
                borrow: 100,
                return: 50
            },
            {
                borrow: 200,
                return: 100
            },
            {
                borrow: 220,
                return: 80
            },
            {
                borrow: 80,
                return: 80
            }
        ]
    }

]


const getBarLength = (bookCount) => {
    // bar max width = 220px  需要拿数组中最大的值进行等比换算 或者 规定一个具体的数字
}

const emit = defineEmits(['current-animation-finish'])
onMounted(() => {
    setTimeout(() => {
        emit('current-animation-finish')
    }, 4000)
})



</script>

<template>
    <div class="monthly-status-page">
        <div class="title-section">
            <div class="title-background"></div>
            <div class="title-box">
                近6月各馆累计借还册次
            </div>
        </div>

        <div class="lib-section">
            <swiper :modules="[Autoplay, Pagination]" :pagination="{el: '.custom-pagination', clickable: true}">
                <swiper-slide v-for="i in 3" :key="`swiper${i}`">
                    <div class="lib-container">
                        <div class="lib-box" v-for="libData in libSwiperList" :key="`${libData.libname}`">
                            <div class="top-section">
                                <div class="title">{{ libData.libname }}</div>
                                <div class="subtitle borrow">借书 {{ libData.borrow }}册</div>
                                <div class="subtitle return">还书 {{ libData.return }}册</div>

                                <div class="lib-image" :style="{backgroundImage: `url(${libData.image})`}"></div>
                            </div>
                            <div class="bottom-section">
                                <div class="month-col">
                                    <div v-for="month in halfYearMonths" :key="`month${month}`">{{ month }}月</div>
                                </div>
                                <!-- compute借阅数量 转成 视图宽度 max 220px -->
                                <div class="graph-box">
                                    <div class="month-row" v-for="(monthData, i) in libData.monthsData"
                                        :key="`month${i}`">
                                        <div class="return">
                                            <div class="bar" :style="{ width: `${monthData.return}px` }"></div>
                                        </div>
                                        <div class="borrow">
                                            <div class="bar" :style="{ width: `${monthData.borrow}px` }"></div>
                                        </div>
                                    </div>
                                </div>
                            </div>

                        </div>
                    </div>
                </swiper-slide>
            </swiper>

            <div class="custom-pagination"></div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.monthly-status-page {
    height: 1216px;
    padding: 70px;
    padding-bottom: 105px;
    /* background-color: #E7F2FF; */
    position: relative;
}

.title-section {
    display: flex;
}

.title-box {
    height: 100px;
    background-color: #fff;
    border-radius: 50px;
    border: 4px solid #3692FF;
    padding: 10px 40px;
    color: #3692FF;
    font-size: 60px;
    line-height: 72px;
    font-weight: 500;
    box-shadow: 28px 15px #3692FF;
}

.lib-section {
    margin-top: 98px;
    padding: 0 24px;
}

:deep(.custom-pagination) {
    position: absolute;
    z-index: 1;
    right: 80px;
    top: 107px;
    left: unset;
    width: auto;
    height: 34px;
    .swiper-pagination-bullet {
        width: 34px;
        height: 34px;
        border-radius: 50%;
        background-color: #fff;
        border: 4px solid #3692FF;
        margin: 0 10px;
    }
    .swiper-pagination-bullet-active {
        background-color: #3692FF;
    }
}

.lib-container {
    display: flex;
    width: 2612px;
    justify-content: space-between;
}

.lib-box {
    width: 608px;
    height: 828px;
    padding: 54px;
    border: 4px solid #3692FF;
    border-radius: 30px;
    background: #fff;
}

.top-section {
    display: flex;
    flex-direction: column;
    margin-bottom: 70px;
    position: relative;

    .title {
        font-size: 48px;
        line-height: 70px;
        font-weight: 700;
        color: #3692FF;
        margin-bottom: 88px;
    }

    .subtitle {
        font-size: 32px;
        line-height: 44px;
        font-weight: 700;

        &:not(:last-child) {
            margin-bottom: 8px;
        }
    }

    .borrow {
        color: #3692FF;
    }

    .return {
        color: #68C945;
    }

    .lib-image {
        position: absolute;
        bottom: 0;
        right: -107px;
        height: 233px;
        width: 350px;
        background-position: center;
        background-repeat: no-repeat;
    }
}

.bottom-section {
    display: flex;

    .month-col {
        /* width: 54px; */
        height: 396px;
        display: flex;
        flex-direction: column;

        >div {
            width: 66px;
            font-size: 32px;
            line-height: 60px;
            color: #88BFFF;
            text-align: justify;

            &:not(:last-child) {
                margin-bottom: 10px;
            }
        }
    }

    .graph-box {
        display: flex;
        flex-direction: column;

        .month-row {
            display: flex;
            margin-bottom: 10px;

            .return,
            .borrow {
                height: 60px;
                width: 220px;

                .bar {
                    height: 60px;
                }
            }

            .return {
                display: flex;
                flex-direction: row-reverse;
                margin-right: 10px;

                .bar {
                    background-color: #68C945;
                    border-radius: 30px 0 0 30px;
                }
            }

            .borrow {
                .bar {
                    background-color: #3692FF;
                    border-radius: 0 30px 30px 0;
                }
            }
        }
    }
}
</style>