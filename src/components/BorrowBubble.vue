<script setup>
import UserBorrowIcon from '@/assets/svg/user-borrow-icon.svg'

const props = defineProps({
    username: {
        type: String,
        default: ''
    },
    libname: {
        type: String,
        default: ''
    },
    position: {
        type: Object,
        default: () => {
            x:0;
            y:0;
        }
    }
})
</script>

<template>
    <div class="borrow-bubble" :style="{left: `${position.x - 61}px`, top: `${position.y - 215}px`}">
        <UserBorrowIcon class="user-icon"/>
        <div class="text">
            <span class="username">{{ username }}</span>
            读者在
            <span class="libname">{{ libname }}</span>
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
    background-size: contain;

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