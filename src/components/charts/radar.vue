<template>
    <div id="container_radar">
        <div id="radar_case"></div>
    </div>
</template>

<script>
import echarts from 'echarts' //引入echarts
export default {
    name: 'comRadar', //组件名
    data(){ //子组件中定义data,必须是一个方法，并返回实例值，data:function(){return{}}
        return {
            myChart: {},
        }
    },
    methods:{//方法
        Init:function() {  //父级div大小改变，图表跟着变化，也可以写成 Init(){}
            window.addEventListener('resize', function() {
                this.myChart.resize()
            }.bind(this))
        }
    },
    mounted() {//生命周期钩子
        this.myChart = echarts.init(document.getElementById("radar_case"));
        let optionData = {
            visualMap: {
                top: 'middle',
                right: 10,
                color: ['#0065cd', '#23c6d5'],
                calculable: true,
                show:false
            },
            radar: {
                indicator : [
                    { text: 'IE8-', max: 400},
                    { text: 'IE9+', max: 400},
                    { text: 'Safari', max: 400},
                    { text: 'Firefox', max: 400},
                    { text: 'Chrome', max: 400}
                ]
            },
            series : (function (){
                var series = [];
                for (var i = 1; i <= 28; i++) {
                    series.push({
                        type: 'radar',
                        symbol: 'none',
                        lineStyle: {
                            width: 1
                        },
                        emphasis: {
                            areaStyle: {
                                color: 'rgba(0,250,0,0.3)'
                            }
                        },
                        data:[
                            {
                            value:[
                                (40 - i) * 10,
                                (38 - i) * 4 + 60,
                                i * 5 + 10,
                                i * 9,
                                i * i /2
                            ],
                            name: i + 2000 + ''
                            }
                        ]
                    });
                }
                return series;
            })()
        };
        this.myChart.setOption(optionData)
        this.Init() //方法调用
    },
}
</script>

<style scoped>
    #container_radar,#radar_case{
        width: 100%;
        height: 100%;
    }
</style>