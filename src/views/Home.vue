<template>
    <div class="container">
        <div  class="column">
            <div class="item one" @click="clickChart('1')" style="transform: translate(-33.5%,-33.5%) scale(0.33)">
                <com-bar></com-bar>
            </div>
            <div class="item two" @click="clickChart('2')" style="transform: translate(-33.5%,0.5%) scale(0.33)">
                <com-line></com-line>
            </div>
            <div class="item three" @click="clickChart('3')" style="transform: translate(-33.5%,34.5%) scale(0.33)">
                <com-pie></com-pie>
            </div>
            <div class="item four active" @click="clickChart('4')" style="transform: translate(34%, 0) scale(1)">
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
            items:[],//用来存放dom节点
        }
    },
    // 方法
    methods: {
        init() {
            this.items = document.querySelectorAll('.item');//获取所有名为.item的节点列表即dom元素
            for (let i = 0; i < this.items.length; i++) {
                this.items[i].dataset.order = i + 1;
                /**
                 * 现在 this.item[i] 是一个 dom 元素
                 * this.items[i].dataset.order 相当于在这个元素上添加一个名为‘data-order’的属性
                 * 因此 this.items[i].dataset.order = i + 1 就等于在该元素上添加了一个‘data-order=i+1’的属性并赋值
                 * .dataset 说明是以data开头，后边的order可以随意更改，也可以添加多个
                 */
            }
        },
        clickChart(num) {
            let activeItem = document.querySelector('.active')//当前展示dom
            let activeIndex = activeItem.dataset.order //展示dom下标
            /**
             * 变量 activeItem 其实是一个dom元素
             * activeItem.dataset.order 表示获取了activeItem上data-order的属性值
             * 但注意，这种方式并不能用来获取自己添加的属性
             */
            let clickItem = this.items[num - 1] //点击dom
            if (activeIndex === num) {
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
        width: 74.7%;
        height: 100%;
        position:absolute;
        text-align: center;
        transition:all 1s;
        background:rgba(105, 105, 105, 0.8);
    }
    .container{
        position: relative;
        width: 100%;
        height :100%;
        display: flex;	            		
        justify-content:center;     		
        align-items:Center;
    }
    .column{
        position: relative;
        height: 90%;
        width: 90%;
        overflow: hidden;
        margin:  0 auto;
    }
    .active{
        height :100%;
        /* width: 75%; */
        line-height: 300px;
    }
</style>
