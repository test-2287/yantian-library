<script setup>
import YanTianMap from '@/assets/svg/full-map.svg'
import CirculateLine from '@/assets/svg/book-circulate-line.svg'
import IconCar from '@/assets/svg/car.svg'



</script>

<template>
    <div class="book-circulate-page">
        <div class="title-section">
            <div class="title-box">盐田区图书流动</div>
        </div>

        <div class="total-data-section">
            <div class="text-1">近6个月数据</div>
            <div class="district-circulate">
                <div class="text-2">区内流动图书数量</div>
                <div class="text-3">35491册</div>
            </div>
            <div class="outflow">
                <div class="text-2">盐田图书馆流出总量</div>
                <div class="text-3">21625册</div>
            </div>
        </div>

        <div class="map-section">
            <YanTianMap />
            <CirculateLine class="circulate-line" />
            <IconCar class="icon-car" />

            <div class="district-data shatoujiao">
                <div class="top">
                    <div>流出图书: 28347册</div>
                    <div>流入图书: 18347册</div>
                </div>
                <div class="bottom lib-name">
                    沙头角街道
                </div>
            </div>

            <div class="district-data yantian">
                <div class="top">
                    <div>流出图书: 28347册</div>
                    <div>流入图书: 18347册</div>
                </div>
                <div class="bottom lib-name">
                    盐田街道
                </div>
            </div>

            <div class="district-data meisha">
                <div class="top">
                    <div>流出图书: 28347册</div>
                    <div>流入图书: 18347册</div>
                </div>
                <div class="bottom lib-name">
                    梅山街道
                </div>
            </div>

            <div class="district-data haishan">
                <div class="top">
                    <div>流出图书: 28347册</div>
                    <div>流入图书: 18347册</div>
                </div>
                <div class="bottom lib-name">
                    海山街道
                </div>
            </div>

        </div>
    </div>


</template>

<style scoped lang="scss">
.book-circulate-page {
    height: 1216px;
    position: relative;
    background-color: #E7F2FF;
    padding: 70px;
}

.title-section {
    display: flex;
}

.title-box {
    height: 100px;
    background-color: #fff;
    border-radius: 50px;
    border: 4px solid #3692FF;
    padding: 10px 40px;
    color: #3692FF;
    font-size: 60px;
    line-height: 72px;
    font-weight: 500;
    box-shadow: 28px 15px #3692FF;
}

.map-section {
    position: absolute;
    top: 100px;
    left: 1040px;

    .circulate-line {
        position: absolute;
        left: 200px;
        bottom: -116px;
    }

    .icon-car {
        position: absolute;
        left: 816px;
        top: 397px;
    }

    .district-data {
        height: 146px;
        border-left: 2px solid #3692FF;
        padding-left: 23px;
        position: absolute;
        white-space: nowrap;

        .top {
            font-size: 24px;
            font-weight: 600;
            line-height: 35px;
            color: #3692FF;
            margin-bottom: 20px;
        }

        .bottom {
            font-size: 36px;
            font-weight: 600;
            line-height: 52px;
            color: #3692FF;
        }
    }

    .shatoujiao {
        top: 413px;
        left: -163px;
    }

    .yantian {
        top: 64px;
        left: 220px;
    }

    .meisha {
        top: 95px;
        left: 1200px;
    }
    .haishan {
        top: 859px;
        left: 1200px;
    }

}

.total-data-section {
    position: absolute;
    top: 552px;
    left: 80px;

    .text-1 {
        font-size: 36px;
        line-height: 52px;
        color: #3692FF;
        font-weight: 500;
    }

    .text-2 {
        font-size: 40px;
        line-height: 58px;
        color: #88BFFF;
        font-weight: 600;
    }

    .text-3 {
        font-size: 96px;
        line-height: 140px;
        color: #3692FF;
        font-weight: 700;
    }

    .district-circulate {
        margin: 34px 0 34px;
        border-top: 6px solid #3692FF;
        border-bottom: 6px solid #3692FF;
        padding: 27px 0 50px;
    }
}
</style>