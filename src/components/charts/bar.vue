<template>
    <div id="container_bar">
        <div id="bar_case"></div>
    </div>
</template>

<script>
import echarts from 'echarts' //引入echarts
export default {
    name: 'comPie',
    data(){
        return{
            legendArr: [],
            myChart:{}
        }
    },
    methods:{
        Init:function() {
            window.addEventListener('resize', function() {
                this.myChart.resize()
            }.bind(this))
        }
    },
    mounted() {
        this.myChart = echarts.init(document.getElementById("bar_case"));
        let optionData = {
            // 图表数据
            color: ['#3398DB'],
            tooltip : {
                trigger: 'axis',
                axisPointer : {            // 坐标轴指示器，坐标轴触发有效
                    type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
                }
            },
            grid: {
                left: '15%',
                top:'10%',
                bottom:'15%',
                right:'10%'
            },
            xAxis : [
                {
                    type : 'category',
                    data : ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                    axisLine: { //坐标轴颜色
                        lineStyle: {
                            color: "#fff",
                        }
                    }
                }
            ],
            yAxis : [
                {
                    type : 'value',
                    axisLine: { //坐标轴颜色
                        lineStyle: {
                            color: "#fff",
                        }
                    }
                }
            ],
            series : {
                name:'平均值',
                type:'bar',
                barWidth: '60%',
                data:[10, 52, 200, 334, 390, 330, 220],
                itemStyle: {
                    normal: {
                        color: new echarts.graphic.LinearGradient(
                            0, 0, 0, 1,
                            [
                                {offset: 0, color: '#1665fe'},
                                {offset: 0.5, color: '#389ffe'},
                                {offset: 1, color: '#54d6ec'}
                            ]
                        ),
                        barBorderRadius: 10
                    },
                },
            }
        };
        this.myChart.setOption(optionData)
        this.Init() //方法调用
    }
}
</script>

<style scoped>
    #container_bar,#bar_case{
        width: 100%;
        height: 100%;
    }
</style>
