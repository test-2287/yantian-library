<script setup>
import { onMounted } from 'vue';


const emit = defineEmits(['current-animation-finish'])
onMounted(() => {
    setTimeout(() => {
        emit('current-animation-finish')
    }, 3000)
})
</script>

<template>
    <div class="top-borrower-page">
        <div class="title-section">
            <div>借书最多的读者</div>
            <div>外借量挑战榜一！</div>
        </div>

        <div class="bubble-box">
            借阅届“卷王”今年已外借134册图书！
        </div>
    </div>
</template>

<style scoped lang="scss">
.top-borrower-page {
    position: relative;
}

.title-section {
    position: absolute;
    top: 97px;
    left: 94px;
    font-size: 64px;
    font-weight: 600;
    line-height: 92.67px;
    color: #3692FF;
    div {
        font-weight: 600;
    }
}

.bubble-box {
    width: 550px;
    height: 298px;
    position: absolute;
    left: 1840px;
    top: 134px;
    background-image: url('@/assets/svg/bubble-515.svg');
    background-size: 550px 298px;
    padding: 43px 50px;
    font-size: 48px;
    font-weight: 600;
    color: #3692FF;
    line-height: 69.5px;
}
</style>