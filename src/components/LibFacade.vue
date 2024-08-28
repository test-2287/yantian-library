<script setup>
import FacadeRoad from '@/assets/svg/facade-road.svg';
import FacadeTree from '@/assets/svg/tree.svg';
import FacadeCloud from '@/assets/svg/cloud.svg';
import Floor from '@/assets/svg/floor.svg';
import FloorB1 from '@/assets/svg/floor-b1.svg';
import FloorF1 from '@/assets/svg/floor-f1.svg';
import FloorF2 from '@/assets/svg/floor-f2.svg';
import FloorF3 from '@/assets/svg/floor-f3.svg';
import WallLeft from '@/assets/svg/wall-left.svg?skipsvgo';
import WallRight from '@/assets/svg/wall-right.svg?skipsvgo';
import FloorPlate from '@/assets/svg/floor-plate.svg';
import B1 from '@/assets/svg/b1.svg?skipsvgo';
import F1 from '@/assets/svg/f1.svg?skipsvgo';
import F2 from '@/assets/svg/f2.svg';
import F3 from '@/assets/svg/f3.svg';
import LibFacade from '@/assets/svg/lib-facade.svg';
import LibLogo from '@/assets/svg/lib-logo.svg';
import IconPeople from '@/assets/svg/icon-people.svg';
import IconHouse from '@/assets/svg/icon-house.svg';
import IconThermometer from '@/assets/svg/icon-thermometer.svg';
import IconStatus from '@/assets/svg/icon-status.svg';

import gsap from 'gsap';
import { ref, onMounted } from 'vue';

const libBox = ref(null);
const showFloors = ref(false);
const currentFloor = ref(0)

const emit = defineEmits(['floor-animation-complete'])


const tl = gsap.timeline();

const tlB1 = () => {

    gsap.set('.libBox', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'center bottom'
    })
    gsap.set('.lib-title-box', {
        opacity: 0,
        x: -465,
    })

    gsap.set('.lib-logo', {
        opacity: 0,
        x: -260
    })
    gsap.set('.lib-condition .condition-box', {
        opacity: 0,
        x: 530
    })
    gsap.set('.road', {
        opacity: 0
    })
    gsap.set('.tree', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'center bottom',
    })
    gsap.set('.cloud1', {
        opacity: 0
    })
    gsap.set('.cloud2', {
        opacity: 0
    })
    gsap.set('.floor-b1', {
        opacity: 0,
        y: -20
    })
    gsap.set('.wall-left', {
        opacity: 0,
        y: 100,
    })
    gsap.set('.wall-right', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-indicator-plate', {
        opacity: 0,
        y: -100
    })
    gsap.set('.floor-indicator-text.b1', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-section-bubble.b1', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'right bottom'
    })

    tl.to('.libBox', {
        opacity: 1,
        scale: 1,
        transformOrigin: 'center bottom',
        duration: 3,
    })
    tl.to('.lib-title-box', {
        opacity: 1,
        x: 0,
        duration: 2
    }, '<')
    tl.to('.lib-logo', {
        opacity: 1,
        x: 0,
        duration: 2
    }, '<')

    tl.to('.road', {
        opacity: 1,
        duration: 2,
    })
    tl.to('.tree', {
        opacity: 1,
        scale: 1,
        transformOrigin: 'center bottom',
        // stagger: 0.8,
        duration: 2,
    }, '<')

    tl.to('.lib-condition .condition-box', {
        opacity: 1,
        x: 0,
        duration: 1,
        stagger: 0.5,
    })

    tl.to('.cloud1', {
        opacity: 1,
        duration: 1
    }, '<')
    tl.to('.cloud1', {
        x: -150,
        y: 100,
        duration: 1.5
    })
    tl.to('.cloud2', {
        opacity: 1,
        duration: 0.5
    }, '<+1.5')

    tl.to('.cloud1', {
        opacity: 0,
        duration: 0.5
    })
    tl.to('.cloud2', {
        x: -242,
        y: 128,
        duration: 2
    }, '<')
    tl.to('.treeGroup1', {
        opacity: 0,
        duration: 0.5
    }, '<+0.5')
    tl.to('.road', {
        opacity: 0,
        duration: 1
    })

    tl.to('.cloud2', {
        opacity: 0,
        duration: 1
    })
    tl.to('.treeGroup2', {
        opacity: 0,
        duration: 2
    }, '<')
    tl.to('.lib', {
        opacity: 0.1,
        duration: 2
    }, '<')

    tl.to('.libFloors', {
        opacity: 1,
        duration: 1
    }, '<+1')

    tl.to('.lib', {
        opacity: 0,
        duration: 1
    })
    tl.to('.lib-condition .condition-box', {
        opacity: 0,
        duration: 1
    }, '<')
    tl.to('.lib-title-box', {
        opacity: 0,
        duration: 1
    }, '<')

    tl.to('.libFloors', {
        scale: 1.4,
        duration: 2,
        transformOrigin: 'center bottom'
    }, '<')

    tl.to('.libFloors', {
        opacity: 0,
        duration: 1,
        onComplete: () => {
            gsap.set('.current-floor-condition .condition-box', {
                opacity: 0,
                x: 530
            })
            showFloors.value = true;
            showFloorText()
        }
    }, '>')

    tl.addLabel('showFloor')

    tl.to('.floor-b1', {
        opacity: 1,
        y: 0,
        duration: 2
    }, '<')

    tl.to('.wall-left', {
        opacity: 1,
        y: 0,
        duration: 1
    })
    tl.to('.wall-right', {
        opacity: 1,
        y: 0,
        duration: 1
    })

    tl.to('.floor-indicator-plate', {
        opacity: 1,
        y: 0,
        duration: 1.5
    }).to('.floor-indicator-text.b1', {
        opacity: 1,
        y: 0,
        duration: 1.5
    })

    tl.to('.current-floor-condition .condition-box', {
        opacity: 1,
        x: 0,
        duration: 1,
        stagger: 0.5
    })

    tl.to('.floor-section-bubble.b1', {
        opacity: 1,
        scale: 1,
        duration: 0.5,
        // stagger: 0.5,
        transformOrigin: 'right bottom'
    })

    tl.addPause('+=2')

    tl.eventCallback('onComplete', () => {
        // tl.tweenTo('showFloor', {
        //     onComplete: () => {
        //         gsap.to('.floor-b1', {
        //             opacity: 0,
        //             y: -20,
        //             duration: 1,
        //             onComplete: () => {
        //                 tlF1()
        //                 currentFloor.value = 1

        //                 // tlF3()
        //                 // currentFloor.value = 3
        //             }
        //         })
        //     }
        // })

        gsap.to(['.floor-section-bubble.b1',
            '.current-floor-condition .condition-box',
            '.floor-indicator-text.b1',
            '.floor-indicator-plate',
            '.wall-right',
            '.wall-left',
            '.floor-b1'], {
            opacity: 0,
            duration: 1,
            onComplete: () => {
                tlF1()
                currentFloor.value = 1
            }
        })

    })
}

const tlF1 = () => {
    const tl = gsap.timeline()

    tl.addLabel('start')

    gsap.set('.floor-f1', {
        opacity: 0,
        y: -20,
    })
    gsap.set('.wall-left', {
        opacity: 0,
        y: 100,
    })
    gsap.set('.wall-right', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-indicator-plate', {
        opacity: 0,
        y: -100
    })
    gsap.set('.floor-indicator-text.f1', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-section-bubble.f1', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'right bottom'
    })
    gsap.set('.current-floor-condition .condition-box', {
        opacity: 0,
        x: 530
    })

    tl.to('.floor-f1', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-left', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-right', {
        opacity: 1,
        y: 0,
        duration: 2
    }, '<+1')

    tl.to('.floor-indicator-plate', {
        opacity: 1,
        y: 0,
        duration: 1.5
    }).to('.floor-indicator-text.f1', {
        opacity: 1,
        y: 0,
        duration: 1.5
    })

    tl.to('.current-floor-condition .condition-box', {
        opacity: 1,
        x: 0,
        duration: 1,
        stagger: 0.5
    })

    tl.to('.floor-section-bubble.f1', {
        opacity: 1,
        scale: 1,
        duration: 0.5,
        // stagger: 0.5,
        transformOrigin: 'right bottom'
    })

    tl.addPause('+=2')

    tl.eventCallback('onComplete', () => {
        // tl.tweenTo('start', {
        //     onComplete: () => {
        //         tlF2()
        //         currentFloor.value = 2
        //     }
        // })

        gsap.to(['.floor-section-bubble.f1',
            '.current-floor-condition .condition-box',
            '.floor-indicator-text.f1',
            '.floor-indicator-plate',
            '.wall-right',
            '.wall-left',
            '.floor-f1'], {
            opacity: 0,
            duration: 1,
            onComplete: () => {
                tlF2()
                currentFloor.value = 2
            }
        })
    })
}

const tlF2 = () => {
    const tl = gsap.timeline()

    tl.addLabel('start')

    gsap.set('.floor-f2', {
        opacity: 0,
        y: -20,
    })
    gsap.set('.wall-left', {
        opacity: 0,
        y: 100,
    })
    gsap.set('.wall-right', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-indicator-plate', {
        opacity: 0,
        y: -100
    })
    gsap.set('.floor-indicator-text.f2', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-section-bubble.f2', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'right bottom'
    })
    gsap.set('.current-floor-condition .condition-box', {
        opacity: 0,
        x: 530
    })

    tl.to('.floor-f2', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-left', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-right', {
        opacity: 1,
        y: 0,
        duration: 2
    }, '<+1')

    tl.to('.floor-indicator-plate', {
        opacity: 1,
        y: 0,
        duration: 1.5
    }).to('.floor-indicator-text.f2', {
        opacity: 1,
        y: 0,
        duration: 1.5
    })

    tl.to('.current-floor-condition .condition-box', {
        opacity: 1,
        x: 0,
        duration: 1,
        stagger: 0.5
    })

    tl.to('.floor-section-bubble.f2', {
        opacity: 1,
        scale: 1,
        duration: 0.5,
        // stagger: 0.5,
        transformOrigin: 'right bottom'
    })

    tl.addPause('+=2')

    tl.eventCallback('onComplete', () => {
        // tl.tweenTo('start', {
        //     onComplete: () => {
        //         tlF3()
        //         currentFloor.value = 3
        //     }
        // })

        gsap.to(['.floor-section-bubble.f2',
            '.current-floor-condition .condition-box',
            '.floor-indicator-text.f2',
            '.floor-indicator-plate',
            '.wall-right',
            '.wall-left',
            '.floor-f2'], {
            opacity: 0,
            duration: 1,
            onComplete: () => {
                tlF3()
                currentFloor.value = 3
            }
        })
    })
}

const tlF3 = () => {
    const tl = gsap.timeline()

    tl.addLabel('start')

    gsap.set('.floor-f3', {
        opacity: 0,
        y: -20,
    })
    gsap.set('.wall-left', {
        opacity: 0,
        y: 100,
    })
    gsap.set('.wall-right', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-indicator-plate', {
        opacity: 0,
        y: -100
    })
    gsap.set('.floor-indicator-text.f3', {
        opacity: 0,
        y: 100
    })
    gsap.set('.floor-section-bubble.f3', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'right bottom'
    })
    gsap.set('.current-floor-condition .condition-box', {
        opacity: 0,
        x: 530
    })

    tl.to('.floor-f3', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-left', {
        opacity: 1,
        y: 0,
        duration: 2
    })
    tl.to('.wall-right', {
        opacity: 1,
        y: 0,
        duration: 2
    }, '<+1')

    tl.to('.floor-indicator-plate', {
        opacity: 1,
        y: 0,
        duration: 1.5
    }).to('.floor-indicator-text.f3', {
        opacity: 1,
        y: 0,
        duration: 1.5
    })

    tl.to('.current-floor-condition .condition-box', {
        opacity: 1,
        x: 0,
        duration: 1,
        stagger: 0.5
    })

    tl.to('.floor-section-bubble.f3', {
        opacity: 1,
        scale: 1,
        duration: 0.5,
        // stagger: 0.5,
        transformOrigin: 'right bottom'
    })

    tl.addPause('+=2')

    tl.eventCallback('onComplete', () => {
        // tl.tweenTo('start', {

        //     onComplete: () => {
        //         gsap.to('.lib-logo', {
        //             opacity: 0,
        //             duration: 1
        //         })
        //         gsap.to('.floor-title-box', {
        //             opacity: 0,
        //             duration: 1
        //         }, '<')
        //         gsap.to('.floor-left-text', {
        //             opacity: 0,
        //             duration: 1
        //         }, '<')


        //         // 切换下一个页面
        //         emit('floor-animation-complete')
        //     }
        // })

        gsap.to(['.floor-section-bubble.f3',
            '.current-floor-condition .condition-box',
            '.floor-indicator-text.f3',
            '.floor-indicator-plate',
            '.wall-right',
            '.wall-left',
            '.floor-f3', 
            '.lib-logo', 
            '.floor-title-box', 
            '.floor-left-text'], {
            opacity: 0,
            duration: 1,
            onComplete: () => {
                emit('floor-animation-complete')
            }
        })
    })
}

const showFloorText = () => {
    const tl = gsap.timeline()
    gsap.set('.floor-title-box', {
        opacity: 0,
        x: -465,
    })
    gsap.set('.floor-left-text', {
        opacity: 0,
        x: -290
    })
    tl.to('.floor-title-box', {
        opacity: 1,
        x: 0,
        duration: 1
    }, '<')

    tl.to('.floor-left-text', {
        opacity: 1,
        x: 0,
        duration: 1
    }, '<')
}


onMounted(() => {
    tlB1()
    // setTimeout(() => {
    //     emit('floor-animation-complete')
    // }, 3000)
});


</script>

<template>
    <div class="lib-facade">

        <div class="title-section">
            <div class="lib-title-box" v-show="!showFloors">盐田图书馆</div>
            <div class="floor-title-box" v-show="showFloors">各楼层展示</div>
        </div>

        <div class="floor-left-text">
            <div class="floor-text" :class="{ current: currentFloor == 4 }">4F</div>
            <div class="floor-text" :class="{ current: currentFloor == 3 }">3F</div>
            <div class="floor-text" :class="{ current: currentFloor == 2 }">2F</div>
            <div class="floor-text" :class="{ current: currentFloor == 1 }">1F</div>
            <div class="floor-text" :class="{ current: currentFloor == 0 }">B1</div>
        </div>

        <LibLogo class="lib-logo" />

        <div class="lib-floor-conditions">
            <div class="lib-condition" v-show="!showFloors">
                <div class="condition-box people-number">
                    <div class="box-left">
                        <IconPeople class="icon-people" />
                        <IconPeople class="icon-people" />
                    </div>
                    <div class="box-right">
                        <div class="label">今日到馆人数</div>
                        <div class="content">359</div>
                    </div>
                </div>
                <div class="condition-box halfyear-arrive">
                    <div class="box-left">
                        <IconStatus class="icon-status" />
                        <IconPeople class="icon-people" />
                    </div>
                    <div class="box-right">
                        <div class="label">近6月到馆人数</div>
                        <div class="content">51126</div>
                    </div>
                </div>
            </div>
            <div class="current-floor-condition" v-show="showFloors">
                <div class="condition-box people-number">
                    <div class="box-left">
                        <IconPeople class="icon-people" />
                        <IconPeople class="icon-people" />
                    </div>
                    <div class="box-right">
                        <div class="label">当前楼层人数</div>
                        <div class="content">252</div>
                    </div>
                </div>
                <div class="condition-box current-temp">
                    <div class="box-left">
                        <IconHouse class="icon-house" />
                        <IconThermometer class="icon-thermometer" />
                    </div>
                    <div class="box-right">
                        <div class="label">当前室内温度</div>
                        <div class="content">15°C</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="page-main">

            <div ref="libBox" class="libBox">
                <LibFacade class="lib" />
            </div>

            <FacadeRoad class="road" />
            <FacadeTree class="tree tree1 treeGroup1" />
            <FacadeTree class="tree tree2 treeGroup1" />

            <FacadeTree class="tree tree3 treeGroup2" />
            <FacadeTree class="tree tree4 treeGroup2" />
            <FacadeTree class="tree tree5 treeGroup2" />

            <FacadeCloud class="cloud cloud1" />
            <FacadeCloud class="cloud cloud2" />

            <div class="libFloors">
                <Floor class="floor" />
                <Floor class="floor" />
                <Floor class="floor" />
                <Floor class="floor" />
            </div>

            <WallLeft class="wall-left" />
            <WallRight class="wall-right" />
            <FloorB1 class="floor-b1" />
            <FloorF1 class="floor-f1" />
            <FloorF2 class="floor-f2" />
            <FloorF3 class="floor-f3" />

            <FloorPlate class="floor-indicator-plate" />
            <B1 class="floor-indicator-text b1" />
            <F1 class="floor-indicator-text f1" />
            <F2 class="floor-indicator-text f2" />
            <F3 class="floor-indicator-text f3" />


            <!-- b1 气泡 -->
            <div class="floor-section-bubble b1 b1-1">
                <div class="label">玩具图书馆</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble b1 b1-2">
                <div class="label">少儿多媒体阅览区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble b1 b1-3">
                <div class="label">少儿图书借阅区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble b1 b1-4">
                <div class="label">服务台</div>
                <div class="content"></div>
            </div>
            <!-- f1 气泡 -->
            <div class="floor-section-bubble f1 f1-1">
                <div class="label">总服务台</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f1 f1-2">
                <div class="label">读海书吧</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f1 f1-3">
                <div class="label">期刊外借区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f1 f1-4">
                <div class="label">报刊阅览区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f1 f1-5">
                <div class="label">视障阅览区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f1 f1-6">
                <div class="label">智慧墙</div>
                <div class="content"></div>
            </div>
            <!-- f2气泡 -->
            <div class="floor-section-bubble f2 f2-1">
                <div class="label">工具书</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f2 f2-2">
                <div class="label">海洋类图书</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f2 f2-3">
                <div class="label">社科综合图书</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f2 f2-4">
                <div class="label">体验区</div>
                <div class="content"></div>
            </div>
            <!-- f3气泡 -->
            <div class="floor-section-bubble f3 f3-1">
                <div class="label">视听播放室</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f3 f3-2">
                <div class="label">电子阅览区</div>
                <div class="content"></div>
            </div>
            <div class="floor-section-bubble f3 f3-3">
                <div class="label">自然科学图书</div>
                <div class="content">6人</div>
            </div>
            <div class="floor-section-bubble f3 f3-4">
                <div class="label">试听服务区</div>
                <div class="content">12人</div>
            </div>
            <div class="floor-section-bubble f3 f3-5">
                <div class="label">创客空间</div>
                <div class="content"></div>
            </div>






        </div>

    </div>
</template>

<style scoped lang="scss">
.lib-facade {
    width: 2828px;
    height: 1216px;
    position: relative;
    display: flex;
    overflow: hidden
}

.title-section {
    position: absolute;
    top: 70px;
    left: 70px;

    .lib-title-box,
    .floor-title-box {
        padding: 10px 43px;
        width: auto;
        height: 100px;
        border-radius: 50px;
        border: 4px solid #3692FF;
        background-color: #fff;
        box-shadow: 15px 15px #3692FF;
        font-size: 60px;
        font-weight: 500;
        line-height: 72px;
        color: #3692FF;
        position: relative;
        opacity: 0;
    }
}

.floor-left-text {
    position: absolute;
    width: 205px;
    height: 329px;
    left: 85px;
    top: 320px;
    opacity: 0;


    .floor-text {
        font-size: 48px;
        font-weight: 500;
        line-height: 65.57px;
        color: #499DFF;
        transition: all ease 1s;

        &.current {
            font-size: 120px;
            font-weight: 600;
            line-height: 163.92px;
        }
    }
}

.lib-logo {
    position: absolute;
    width: 190px;
    height: 296px;
    top: 808.21px;
    left: 95px;
    opacity: 0;
}

.lib-floor-conditions {
    position: absolute;
    top: 70px;
    right: 85px;

    .condition-box {
        width: 460px;
        height: 200px;
        padding: 22px 40px;
        border-radius: 40px;
        border: 3px solid #3692FF;
        background-color: #fff;
        margin-bottom: 55px;
        display: flex;
        align-items: flex-end;
        justify-content: space-between;
        box-shadow: 15px 15px #C0DDFF;
        opacity: 0;

        .box-left {
            display: flex;
            align-items: flex-end;
            margin-bottom: 15px;
        }

        .box-right {
            text-align: right;
            display: flex;
            flex-direction: column;
            justify-content: space-between;

            .label {
                font-size: 32px;
                font-weight: 500;
                line-height: 38.4px;
                color: #88BFFF;

            }

            .content {
                font-size: 80px;
                font-weight: 600;
                line-height: 109.28px;
                color: #3692FF;
            }
        }
    }

    .people-number {
        .icon-people {
            width: 64px;
            height: 91px;
            margin-right: -16px;
        }
    }

    .halfyear-arrive {
        .icon-status {
            width: 80px;
            height: 97px;
            margin-right: -16px;
        }

        .icon-people {
            width: 46px;
            height: 65px;
        }
    }

    .current-temp {
        .icon-house {
            width: 80px;
            height: 112px;
            margin-right: -16px;
        }

        .icon-thermometer {
            width: 34px;
            height: 70px;
        }
    }
}

.page-main {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    height: 1216px;
    min-width: 1124px;
}

.libBox {
    opacity: 0;
}

.lib {
    width: 1124px;
    height: 1134px;
    padding-top: 32px;
}

.road,
.tree,
.cloud {
    position: absolute;
    opacity: 0;
}

.road {
    position: absolute;
    z-index: -1;
    right: 430px;
    bottom: -6px;
}

.tree {
    width: 123px;
    height: 200px;
}

.tree1 {
    left: -360px;
    top: 450px;
}

.tree2 {
    left: -250px;
    top: 398px;
}

.tree3 {
    right: -60px;
    bottom: 200px;
}

.tree4 {
    right: -142px;
    bottom: 240px;
}

.tree5 {
    right: -225px;
    bottom: 280px;
}

.cloud1 {
    width: 175px;
    height: 175px;
    left: -215px;
    top: 83px;
}

.cloud2 {
    width: 258px;
    height: 258px;
    right: -220px;
    bottom: 480px;
}

.libFloors {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 155px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: space-between;
    opacity: 0;
}

.floor {
    width: 1100px;
    transform: skew(6deg, 2deg) scale(1.02);
    position: relative;

    &:not(:last-child) {
        margin-top: -458px;
    }

}

.floor-b1,
.floor-f1,
.floor-f2,
.floor-f3 {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) skew(0, 1deg);
    bottom: 26px;
    opacity: 0;
}

/* .floor-f2 {
    opacity: 1;
} */

.wall-left,
.wall-right {
    position: absolute;
    opacity: 0;
}

.wall-left {
    width: 756px;
    height: 917px;
    top: 0;
    left: -382px;
}

.wall-right {
    width: 784px;
    height: 990px;
    bottom: -195px;
    right: -245px;
}

.floor-indicator-plate {
    position: absolute;
    right: -100px;
    bottom: 150px;
    width: 346px;
    height: 268px;
    right: -460px;
    bottom: 50px;
    opacity: 0;
}

.floor-indicator-text {
    position: absolute;
    width: 204px;
    height: 321px;
    right: -383px;
    bottom: 125px;
    opacity: 0;

    &.b1,
    &.f1,
    &.f2,
    &.f3 {
        opacity: 0;
    }
}


.floor-section-bubble {
    position: absolute;
    width: 260px;
    height: 160px;
    border: 4px solid #3692FF;
    border-radius: 30px;
    box-shadow: 10px 10px rgba(54, 146, 255, 0.3);
    background: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    opacity: 0;

    &.bubble-right {
        border-bottom-right-radius: 0;
    }

    &.bubble-left {
        border-bottom-left-radius: 0;
    }

    .label {
        font-size: 30px;
        font-weight: 700;
        line-height: 36px;
        text-align: center;
        color: #499DFF;
    }

    .content {
        font-size: 50px;
        font-weight: 600;
        line-height: 68.3px;
        text-align: center;
        color: #3692FF;
    }

    &.b1-1 {
        top: 463px;
        left: -145px;
    }

    &.b1-2 {
        top: 220px;
        left: 260px;
    }

    &.b1-3 {
        top: 368px;
        left: 760px;
    }

    &.b1-4 {
        top: 863px;
        left: 429px;
    }

    &.f1-1 {
        top: 800px;
        left: 266px;
    }

    &.f1-2 {
        top: 406px;
        left: -158px;
    }

    &.f1-3 {
        top: 260px;
        left: 260px;
    }

    &.f1-4 {
        top: 350px;
        left: 740px;
    }

    &.f1-5 {
        top: 955px;
        left: 860px;
    }

    &.f1-6 {
        top: 537px;
        left: 340px;
    }

    /* &.f2 {
        opacity: 1;
    } */
    &.f2-1 {
        top: 757px;
        left: 320px;
    }

    &.f2-2 {
        top: 350px;
        left: 50px;
    }

    &.f2-3 {
        top: 240px;
        left: 570px;
    }

    &.f2-4 {
        top: 838px;
        left: 960px;
    }

    &.f3-1 {
        top: 773px;
        left: 180px;
    }

    &.f3-2 {
        top: 300px;
        left: 0px;
    }

    &.f3-3 {
        top: 228px;
        left: 500px;
    }

    &.f3-4 {
        top: 469px;
        left: 900px;
    }

    &.f3-5 {
        top: 934px;
        left: 880px;
    }


}
</style>