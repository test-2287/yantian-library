<script setup>
const props = defineProps({
    libName: {
        type: String,
        default: ''
    },
    humidity: {
        type: Number,
        default: 0
    },
    airQuality: {
        type: String,
        default: ''
    },
    position: {
        type: Object,
        default: () => {
            x: 0
            y: 0
        }
    }
})
</script>

<template>
    <div class="lib-condition-bubble" :style="{ left: `${position.x - 125}px`, top: `${position.y - 215}px` }">
        <div class="lib-name">{{ libName }}</div>
        <div class="lib-condition">
            <div class="item">
                <div class="item-label">温湿度</div>
                <div class="item-desc">{{ humidity }}°</div>
            </div>
            <div class="item">
                <div class="item-label">空气质量</div>
                <div class="item-desc">
                    <span>良好 </span>
                    <i></i>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped lang="scss">
.lib-condition-bubble {
    position: absolute;
    width: 250px;
    height: 190px;
    padding: 16px 20px;
    padding-bottom: 24px;
    background-image: url('@/assets/svg/lib-condition-bubble.svg');
    background-size: 250px 190px;
}

.lib-name {
    font-size: 24px;
    line-height: 35px;
    color: #3692FF;
    font-weight: 700;
    margin-bottom: 16px;
}

.lib-condition .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 20px;
    line-height: 29px;
    font-weight: 700;
    &:not(:last-child) {
        margin-bottom: 12px;
    }
    .item-label {
        color: #88BFFF;
    }
    .item-desc {
        color: #3692FF;
    }
}
</style>