<script setup>
import FacadeRoad from '@/assets/svg/facade-road.svg';
import FacadeTree from '@/assets/svg/tree.svg';
import FacadeCloud from '@/assets/svg/cloud.svg';
import Floor from '@/assets/svg/floor.svg';
import FloorB1 from '@/assets/svg/floor-b1.svg';
import FloorF1 from '@/assets/svg/floor-f1.svg';
import WallLeft from '@/assets/svg/wall-left.svg?skipsvgo';
import WallRight from '@/assets/svg/wall-right.svg?skipsvgo';
import FloorPlate from '@/assets/svg/floor-plate.svg';
import B1 from '@/assets/svg/b1.svg?skipsvgo';
import F1 from '@/assets/svg/f1.svg?skipsvgo';
import LibFacade from '@/assets/svg/lib-facade.svg';

import gsap from 'gsap';
import { ref, onMounted, nextTick } from 'vue';

// const emit = defineEmits(['animation-complete'])

const libBox = ref(null);

const tl = gsap.timeline();

const tlB1 = () => {

    gsap.set('.libBox', {
        opacity: 0,
        scale: 0,
        transformOrigin: 'center bottom'
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

    tl.to('.libBox', {
        opacity: 1,
        scale: 1,
        transformOrigin: 'center bottom',
        duration: 3,
    })
    tl.to('.road', {
        opacity: 1,
        duration: 3,
    })
    tl.to('.tree', {
        opacity: 1,
        scale: 1,
        transformOrigin: 'center bottom',
        stagger: 0.8,
        duration: 3,
    }, '<')

    tl.to('.cloud1', {
        opacity: 1
    }).to('.cloud1', {
        x: -150,
        y: 100,
        duration: 2
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

    tl.to('.libFloors', {
        scale: 1.4,
        duration: 2,
        transformOrigin: 'center bottom'
    }, '<')

    tl.to('.libFloors', {
        opacity: 0,
        duration: 1,
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

    tl.eventCallback('onComplete', () => {
        tl.tweenTo('showFloor', {
            onComplete: () => {
                gsap.to('.floor-b1', {
                    opacity: 0,
                    y: -20,
                    duration: 1,
                    onComplete: () => {
                        tlF1()
                    }
                })
            }
        })
    })
}

const tlF1 = () => {
    const tl = gsap.timeline({
        onComplete: () => {
            tl.tweenFromTo('start', {
                onComplete: () => {

                }
            })
            tlF2();
        }
    })

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

    tl.eventCallback('onComplete', () => {
        tl.tweenTo('start', {
            onComplete: () => {
                tlF2()
            }
        })
    })
}

const tlF2 = () => {
    console.log('f2');
 }

onMounted(() => {
    tlB1()
    // tlF1()
});



</script>

<template>
    <div class="lib-facade">
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

            <FloorPlate class="floor-indicator-plate" />
            <B1 class="floor-indicator-text b1" />
            <F1 class="floor-indicator-text f1" />




        </div>

    </div>
</template>

<style scoped>
.lib-facade {
    width: 2828px;
    height: 1216px;
    position: relative;
    display: flex;
    overflow: hidden
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
.floor-f1 {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) skew(0, 1deg);
    bottom: 26px;
    opacity: 0;
}

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

    &.f1 {
        opacity: 0;
    }
}
</style>