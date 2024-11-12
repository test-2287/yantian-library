<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'
import { onMounted } from 'vue';

const emit = defineEmits(['current-animation-finish'])
onMounted(() => {
    setTimeout(() => {
        emit('current-animation-finish')
    }, 3000)
})

</script>

<template>
    <div class="new-user-page">
        <div class="title-section">
            <div class="left-section">新增持证读者，终于等到你！</div>
            <div class="right-section">
                <div>盐图今年新增</div>
                <div>18364位读书人</div>
            </div>
        </div>

        <div class="map-section">
            <YanTianMap />
        </div>

        <div class="congrats-bubble">
            祝贺李**在盐田图书馆成功办理盐图读者证
        </div>
    </div>
</template>

<style scoped lang="scss">
.new-user-page {
    height: 1216px;
    padding: 90px;
    position: relative;
}

.title-section{
    display: flex;
    justify-content: space-between;
    font-size: 64px;
    line-height: 94px;
    font-weight: 700;
    color: #3692FF;
    .right-section {
        text-align: right;
    }
    div {
        font-weight: 700;
    }
}

.map-section {
    position: absolute;
    top: 125px;
    /* left: 1056px; */
    right: 120px;
}

.congrats-bubble {
    position: absolute;
    top: 323px;
    left: 616px;
    width: 515px;
    height: 298px;
    padding: 52px;
    padding-bottom: 116px;
    background-image: url('@/assets/svg/bubble-515.svg');
    background-size: cover;

    font-size: 40px;
    line-height: 58px;
    font-weight: 600;
    color: #3692FF;
}
</style>
