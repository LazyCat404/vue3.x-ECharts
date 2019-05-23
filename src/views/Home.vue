<template>
    <div class="dashboard">
        <div  class="column">
            <div class="item one" @click="clickChart('1')" style="transform: translate(-22.4%,-33.5%) scale(0.33)">
                <com-bar></com-bar>
            </div>
            <div class="item two" @click="clickChart('2')" style="transform: translate(-22.4%,0.5%) scale(0.33)">
                <com-line></com-line>
            </div>
            <div class="item three" @click="clickChart('3')" style="transform: translate(-22.4%,34.5%) scale(0.33)">
                <com-pie></com-pie>
            </div>
            <div class="item four active" @click="clickChart('4')" style="transform: translate(43.7%, 0) scale(1)">
                <com-radar></com-radar>
            </div>
        </div>
    </div>
</template>

<script>
import comBar from '@/components/charts/bar'
import comLine from '@/components/charts/line'
import comPie from '@/components/charts/pie'
import comRadar from '@/components/charts/radar'
export default {
    name: 'Home',
    // 组件注册
    components: {
        'com-bar': comBar,
        'com-line': comLine,
        'com-pie': comPie,
        'com-radar': comRadar,
    },
    data() {
        return{
            items:[],
        }
    },
    // 方法
    methods: {
        init() {
            this.items = document.querySelectorAll('.item')
            for (let i = 0; i < this.items.length; i++) {
                this.items[i].dataset.order = i + 1;
            }
        },
        clickChart(clickIndex) {
            let activeItem = document.querySelector('.active')
            let activeIndex = activeItem.dataset.order
            let clickItem = this.items[clickIndex - 1]
            if (activeIndex === clickIndex) {
                return
            }
            activeItem.classList.remove('active')
            clickItem.classList.add('active')
            this.setStyle(clickItem, activeItem)
        },
        setStyle(el1, el2) {
            let transform1 = el1.style.transform
            let transform2 = el2.style.transform
            el1.style.transform = transform2
            el2.style.transform = transform1
        }
    },
    mounted(){
        this.init()
    }
}
</script>

<style scoped>
    .item{
        padding: 0px;
        margin: 0px;
        width: 68%;
        height: 100%;
        position:absolute;
        transform :scale(0.33);
        text-align: center;
        transition:all 0.8s;
        background:rgba(105, 105, 105, 0.8);
    }
    .dashboard{
        position: relative;
        width: 100%;
        height :100%;
        margin:0px;
        padding:0px;
        padding-top: 5%;
        background-size: 100% 100%;
    }
    .column{
        position: relative;
        height: 90%;
        width: 90%;
        overflow: hidden;
        margin:  0 auto 0px auto;
        box-sizing: content-box;
    }
    .active{
        height :100%;
        width: 69%;
        margin-left: 10px;
        line-height: 300px;
    }
</style>
