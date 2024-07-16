<script setup>
import LibFacade from './LibFacade.vue';
import FloorOne from './FloorOne.vue';

import { defineComponent, onMounted, ref } from 'vue';

defineComponent

const animationOrder = {
    LibFacade,
    FloorOne,
}
const animationArray = [
    'LibFacade',
    'FloorOne',
]

const currentFloor = ref(0);

const onAnimationUpdate = () => {
    if (currentFloor.value === animationArray.length - 1) {
        currentFloor.value = 0;
    } else {
        currentFloor.value++
    }   
}

onMounted(() => {
    // console.log(currentFloor.value)
    // console.log(animationArray.value[0])
    // console.log(animationOrder.value[animationArray.value[currentFloor.value]])
})

</script>

<template>

    <div class="section-floors">

        <!-- <LibFacade /> -->
        <!-- <FloorOne></FloorOne> -->
        <component :is="animationOrder[animationArray[currentFloor]]" 
        v-on:animation-complete="onAnimationUpdate"
        />

    </div>
</template>

<style scoped>
.section-floors {
    overflow: hidden;
    width: 2828px;
    height: 1216px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #E7F2FF;
}
</style>