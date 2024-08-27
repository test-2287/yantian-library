<script setup>
import { ref, onMounted } from 'vue';
// import { shuffle as _shuffle } from 'lodash-es';


let arriveData = ref([
    {
        id: 0,
        name: '沙头角街道图书馆',
        number: 3172
    },
    {
        id: 1,
        name: '中英街图书馆',
        number: 2310
    },
    {
        id: 2,
        name: '灯塔图书馆',
        number: 2192
    },
    {
        id: 3,
        name: '邂逅图书馆',
        number: 1320
    },
    {
        id: 4,
        name: '遇见图书馆',
        number: 1280
    },
    {
        id: 5,
        name: '盐田图书馆',
        number: 1000
    },
    {
        id: 6,
        name: '海山街道图书馆',
        number: 1202
    },
    {
        id: 7,
        name: '春天海图书馆',
        number: 931
    },
    {
        id: 8,
        name: '望海街道图书馆',
        number: 880
    },
    {
        id: 9,
        name: '沙头角街道图书馆',
        number: 569
    },
    {
        id: 10,
        name: '沙头角街道图书馆',
        number: 569
    },
    {
        id: 11,
        name: '沙头角街道图书馆',
        number: 569
    },
    {
        id: 12,
        name: '沙头角街道图书馆',
        number: 569
    },
    {
        id: 13,
        name: '沙头角街道图书馆',
        number: 569
    }
])


// const shuffle = () => {
//     arriveData.value = _shuffle(arriveData.value)
// }

const updateData = () => {
    arriveData.value.forEach(item => {
        item.number = Math.floor(Math.random() * 5000)
    })
}

const sortData = () => {
    arriveData.value.sort((a, b) => b.number - a.number)
    setBarLength()
}

const setBarLength = () => {
    let max = Math.max(...arriveData.value.map(item => item.number))
    let widthRatio = 1094 / max;
    arriveData.value.forEach(item => {
        item.barWidth = parseInt(item.number * widthRatio)
    })
    // console.log(arriveData);
}


const emit = defineEmits(['current-animation-finish'])

onMounted(() => {
    // setBarLength()
    sortData()
    setTimeout(() => {
        // shuffle()
        updateData()
        sortData()
    }, 3000)

    setTimeout(() => {
        emit('current-animation-finish')
    }, 5000)
})



</script>

<template>
    <div class="page-today-arrive">

        <div class="blue-layer">

            <div class="title-section">
                <div class="top-section">
                    <div>1月到6月</div>
                    <div>累计到馆</div>
                </div>
                <div class="bottom-section">
                    32982人
                </div>
            </div>

            <div class="light-blue-layer">
                <!-- <div class="arrive-ranking-list"> -->
                <TransitionGroup name="list" tag="div" class="arrive-ranking-list">
                    <div v-for="item in arriveData" :key="item.id" class="arrive-item">
                        <div class="arrive-item-name ">{{ item.name }}</div>
                        <div class="arrive-item-right">
                            <div class="arrive-item-bar"
                                :style="{ width: item.barWidth ? `${item.barWidth}px` : '200px' }"></div>
                            <div class="arrive-item-number">{{ item.number }}</div>
                        </div>
                    </div>
                </TransitionGroup>
                <!-- </div> -->
            </div>
        </div>
    </div>
</template>

<style scoped>
.page-today-arrive {
    width: 2828px;
    height: 1216px;
    /* background-color: #E7F2FF; */
    position: relative;
    overflow: hidden;
}

.blue-layer {
    position: relative;
    width: 2828px;
    height: 1216px;
    /* background-color: #C0DDFF; */
    /* clip-path: ellipse(2828px 1300px at 1950px 530px); */
    /* transition: all ease cubic-bezier(0.55, 0.055, 0.675, 0.19) */
}

.light-blue-layer {
    width: 2130px;
    height: 1216px;
    /* background-color: #E7F2FF; */
    position: absolute;
    right: 0;
    top: 0;
    /* clip-path: ellipse(1950px 1300px at 1950px 530px); */
    /* transition: all ease cubic-bezier(0.55, 0.055, 0.675, 0.19)transition: all ease cubic-bezier(0.55, 0.055, 0.675, 0.19) */

    /* clip-path: circle(2130px at 1950px 530px); */

}

.arrive-ranking-list {
    width: 1600px;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    right: 200px;

    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    height: 1160px;
}

.arrive-item {
    width: 1600px;
    height: 60px;
    /* margin-bottom: 40px; */
    display: flex;

}

.arrive-item-name {
    width: 320px;
    flex-basis: 320px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    margin-right: 40px;
    text-align: right;
    font-size: 36px;
    line-height: 40px;
    font-weight: 600;
    color: #3692FF;
}

.left-wrapper {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    margin-right: 40px;
}

.right-wrapper {
    margin-left: 40px;
}

.arrive-item-right {
    display: flex;
}

.arrive-item-bar {
    height: 60px;
    width: 600px;
    max-width: 1094px;
    border-radius: 30px;
    border: 3px solid #3692FF;
    background-color: #fff;
    transition: all 2s ease;
}

.arrive-item-number {
    margin-left: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 40px;
    line-height: 55px;
    font-weight: 700;
    color: #3692FF;
}

.list-move,
.list-enter-active,
.list-leave-active {
    transition: all 2s cubic-bezier(0.55, 0, 0.1, 1);
}

/* .list-enter-from, list-enter-to {
    opacity: 0;
    transform: translateY(-100px);
} */


.title-section {
    padding: 80px 90px;
    .top-section {
        width: 360px;
        padding-bottom: 22px;
        margin-bottom: 22px;
        border-bottom: 4px solid #3692FF;
        font-size: 64px;
        line-height: 93px;
        font-weight: 600;
        color: #3692FF;
    }
    .bottom-section {
        font-size: 80px;
        line-height: 109px;
        font-weight: 600;
        color: #3692FF;
    }
}
</style>