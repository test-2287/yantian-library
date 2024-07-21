<script setup>
import qrCodeService from '@/assets/svg/qrcode-service.svg';
import qrCodeSubscribe from '@/assets/svg/qrcode-subscribe.svg';
</script>

<template>
    <div class="new-user-page">
        <div class="title-section">
            <div class="left-section">新增持证读者，终于等到你！</div>
            <div class="right-section">
                <div>本月新增2823位网上邻居</div>
                <div>关注了盐图微信公众号</div>
            </div>
        </div>

        <div class="qrcode-section">
            <div class="code-container">
                <div class="code-box">
                    <div class="code-image">
                        <qrCodeService />
                    </div>
                </div>
                <div class="desc-text">微信服务号</div>
            </div>
            <div class="code-container">
                <div class="code-box">
                    <div class="code-image">
                        <qrCodeSubscribe />
                    </div>
                </div>
                <div class="desc-text">微信订阅号</div>
            </div>
        </div>

        <div class="bubble-box">
            让我看看是谁还没有关注盐图的微信公众号？
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
}

.qrcode-section {
    position: absolute;
    top: 376px;
    left: 292px;

    display: flex;
    .code-container {
        margin-right: 165px;
        .code-box {
            width: 400px;
            height: 400px;
            border-radius: 30px;
            border: 4px solid #3692FF;
            display: flex;
            justify-content: center;
            align-items: center;
            .code-image {
                width: 350px;
                height: 350px;
            }
        }
        .desc-text {
            text-align: center;
            margin-top: 50px;
            font-size: 48px;
            line-height: 70px;
            font-weight: 600;
            color: #3692FF;
        }
    }
}



.bubble-box {
    position: absolute;
    top: 715px;
    left: 1480px;
    width: 607px;
    height: 325px;
    padding: 60px;
    padding-right: 150px;
    background-image: url('@/assets/svg/bubble-607.svg');
    background-repeat: no-repeat;
    background-size: cover;

    font-size: 48px;
    line-height: 70px;
    font-weight: 600;
    color: #3692FF;
}
</style>
