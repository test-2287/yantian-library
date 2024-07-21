<script setup>
import UserBorrowIcon from '@/assets/svg/user-borrow-icon.svg'

const props = defineProps({
    username: {
        type: String,
        default: ''
    },
    libName: {
        type: String,
        default: ''
    },
    x: {
        type: Number,
        default: 0
    },
    y : {
        type: Number,
        default: 0
    }
})
</script>

<template>
    <div class="borrow-bubble" :style="{left: `${x - 61}px`, top: `${y - 215}px`}">
        <UserBorrowIcon class="user-icon"/>
        <div class="text">
            <span class="username">{{ username }}</span>
            读者在
            <span class="libname">{{ libName }}</span>
            外借图书
        </div>
    </div>
</template>

<style scoped lang="scss">
.borrow-bubble {
    position: absolute;
    width: 382px;
    height: 180px;
    padding: 32px 27px;
    background-image: url('@/assets/svg/user-borrow-bubble.svg');
    background-size: cover;
    /* opacity: 0; */

    .user-icon {
        width: 64px;
        height: 64px;
        position: absolute;
        top: -30px;
        left: -30px;
    }

    .text {
        font-size: 32px;
        line-height: 46px;
        color: #C0DDFF;
        font-weight: 600;
    }
    .username, .libname{
        color: #3692FF;
    }

}
</style>