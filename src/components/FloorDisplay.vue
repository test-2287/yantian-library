<script setup>
import LibFacade from '@/components/LibFacade.vue'

const emit = defineEmits(['current-animation-finish'])

const floorAnimationFinish = () => {
    console.log('floor animation complete');
    emit('current-animation-finish')
}

</script>

<template>

    <div class="section-floors">

        <LibFacade @floor-animation-complete="floorAnimationFinish"/>

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