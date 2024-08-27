<script setup>
import gsap from 'gsap';
// import FloorOne from '@/assets/svg/floor-1.svg';
import WallLeft from '@/assets/svg/wall-left.svg?skipsvgo';
import WallRight from '@/assets/svg/wall-right.svg?skipsvgo';
import FloorPlate from '@/assets/svg/floor-plate.svg';
// import OneFloor from '@/assets/svg/1f.svg?skipsvgo';

import { onMounted } from 'vue';

const tl = gsap.timeline();

defineEmits(['animation-complete']);

onMounted(() => {
    tl.from('.floor-1', {
        opacity: 0,
        y: -20,
        duration: 1
    }).from('.wall-left', {
        opacity: 0,
        y: 100,
        duration: 1
    }).from('.wall-right', {
        opacity: 0,
        y: 100,
        duration: 1
    }).from('.floor-indicator-plate', {
        opacity: 0,
        y:-100,
        duration: 1
    }).from('.floor-indicator-text', {
        opacity: 0,
        y: 100,
        duration: 1
    })

    tl.to('.floor-1', {
        opacity: 1,
        y: 0,
    }).to('.wall-left', {
        opacity: 1,
        y: 0,
    }).to('.wall-right', {
        opacity: 1,
        y: 0,
    }).to('.floor-indicator-plate', {
        opacity: 1,
        y: 0,
    }).to('.floor-indicator-text', {
        opacity: 1,
        y: 0,
    })

})
</script>

<template>
    <div class="lib-1">
        <WallLeft class="wall-left" />
        <WallRight class="wall-right" />
        <FloorOne class="floor-1" />

        <FloorPlate class="floor-indicator-plate" />
        <OneFloor class="floor-indicator-text" />
    </div>
</template>

<style scoped>
.lib-1 {
    position: relative;
    top: 0;
    height: 1216px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.wall-left {
    position: absolute;
    top: 0;
    left: -70px;
}

.wall-right {
    position: absolute;
    bottom: -80px;
    right: 0;
}

.floor-1 {
    position: relative;
}

.floor-indicator-plate {
    position: absolute;
    bottom: 168px;
    right: -400px;
    transform: translateX(-50%);
}

.floor-indicator-text {
    position: absolute;
    bottom: 250px;
    right: -250px;
    transform: translateX(-50%);
}
</style>