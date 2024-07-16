<script setup>
import LibFacade from '@/assets/svg/lib-facade.svg';
import FacadeRoad from '@/assets/svg/facade-road.svg';
import FacadeTree from '@/assets/svg/tree.svg';
import FacadeCloud from '@/assets/svg/cloud.svg';
import Floor from '@/assets/svg/floor.svg';
import FloorB1 from '@/assets/svg/floor-b1.svg';
import WallLeft from '@/assets/svg/wall-left.svg?skipsvgo';
import WallRight from '@/assets/svg/wall-right.svg?skipsvgo';
import FloorPlate from '@/assets/svg/floor-plate.svg';
import BOne from '@/assets/svg/b1.svg?skipsvgo';

import gsap from 'gsap';
import { ref, onMounted } from 'vue';

const libBox = ref(null);

const tl = gsap.timeline();

const emit = defineEmits(['animation-complete'])

onMounted(() => {

    // tl.from(libBox.value, {
    //     opacity: 0,
    //     scale: 0,
    //     transformOrigin: 'center bottom',
    //     duration: 3,
    // })

    // tl.from('.road', {
    //     opacity: 0,
    //     duration: 3,
    // })

    // tl.from('.tree', {
    //     opacity: 0,
    //     scale: 0,
    //     transformOrigin: 'center bottom',
    //     stagger: 0.8,
    //     duration: 3,
    // }, '-=3')

    // tl.from('.cloud1', {
    //     opacity: 0
    // })

    // tl.to('.cloud1', {
    //     opacity: 1
    // }).to('.cloud1', {
    //     x: -150,
    //     y: 100,
    //     duration: 2
    // })

    // tl.from('.cloud2', {
    //     opacity: 0
    // }, "-=1.5")
    // tl.to('.cloud2', {
    //     opacity: 1
    // }).to('.cloud1', {
    //     opacity: 0
    // }).to('.cloud2', {
    //     x: -150,
    //     y: 100,
    //     duration: 1
    // }, '-=1')

    // tl.to('.treeGroup1', {
    //     opacity: 0,
    //     duration: 1.5
    // }, '-=2').to('.road', {
    //     opacity: 0,
    //     duration: 1.5
    // }, '-=2').to('.lib', {
    //     opacity: 0.1,
    //     duration: 4
    // }).to('.treeGroup2', {
    //     opacity: 0,
    //     duration: 1.5
    // }, '-=2.5').to('.cloud2', {
    //     opacity: 0,
    //     duration:0.6
    // }, '-=2.5')

    tl.from('.libFloors', {
        opacity: 0,
        duration: 2
    }, '-=1.5').to('.libFloors', {
        opacity: 1
    })
        .to('.lib', {
            opacity: 0,
            duration: 1.5
        })
        .to('.libFloors', {
            scale: 1.4,
            duration: 2,
            transformOrigin: 'center bottom'
        }, '<')


    tl.from('.floor-b1', {
        opacity: 0,
        y: -20,
        duration: 2
    })

    tl.addLabel('showFloor')

    tl.from('.wall-left', {
        opacity: 0,
        y: 100,
        duration: 2
    }).from('.wall-right', {
        opacity: 0,
        y: 100,
        duration: 2
    })




    tl.to('.floor-b1', {
        opacity: 1,
        y: 0,
    })
        // .to('.libFloors', {
        //     opacity: 0,
        //     duration: 3
        // }, '<-5')
        .to('.wall-left', {
            opacity: 1,
            y: 0,
            duration: 0.5
        }, '<').to('.wall-right', {  //<-2.8
            opacity: 1,
            y: 0,
            duration: 0.5,
        }, '<+0.5')         // <+2
        .to('.libFloors', {
            opacity: 0,
            duration: 3
        }, '<-7')



    tl.from('.floor-indicator-plate', {
        opacity: 0,
        y: -100,
        duration: 1.5
    }).from('.floor-indicator-text', {
        opacity: 0,
        y: 100,
        duration: 1.5
    }).to('.floor-indicator-plate', {
        opacity: 1,
        y: 0
    }).to('.floor-indicator-text', {
        opacity: 1,
        y: 0
    })


    tl.eventCallback('onComplete', () => {
        tl.tweenTo('showFloor', {
            onComplete: () => {
                gsap.to('.floor-b1', {
                    opacity: 0,
                    y: -20,
                    duration: 2,
                    onComplete: () => {
                        emit('animation-complete')
                    }
                })
            }
        })
    })

});

</script>

<template>
    <div class="lib-facade">
        <div class="page-main">
            <div ref="libBox">
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

            <FloorPlate class="floor-indicator-plate" />
            <BOne class="floor-indicator-text" />


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

.lib {
    width: 1124px;
    height: 1134px;
    padding-top: 32px;
}

.road,
.tree,
.cloud {
    position: absolute;
}

.road {
    position: absolute;
    z-index: -1;
    right: 430px;
    bottom: -6px;
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
    right: 20px;
    bottom: 85px;
}

.tree4 {
    right: -90px;
    bottom: 140px;
}

.tree5 {
    right: -200px;
    bottom: 196px;
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
    right: -650px;
    bottom: 210px;
}

.libFloors {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 155px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: space-between;
}

.floor {
    width: 1100px;
    transform: skew(6deg, 2deg) scale(1.02);
    position: relative;

    &:not(:last-child) {
        margin-top: -458px;
    }
}

.floor-b1 {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) skew(0, 1deg);
    bottom: 26px;
}

.wall-left,
.wall-right {
    position: absolute;
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
}

.floor-indicator-text {
    position: absolute;
    width: 204px;
    height: 321px;
    right: -383px;
    bottom: 125px;
}
</style>