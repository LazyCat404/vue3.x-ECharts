<template>
    <div id="container_pie">
        <div id="pie_case"></div>
    </div>
</template>

<script>
import echarts from 'echarts' //引入echarts
export default {
    name: 'comPie',
    data(){
        return{
            myChart:{}
        }
    },
    methods:{
        Init:function() {  //父级div大小改变，图表跟着变化，也可以写成 Init(){}
            window.addEventListener('resize', function() {
                this.myChart.resize()
            }.bind(this))
        }
    },
    mounted() {
        this.myChart = echarts.init(document.getElementById("pie_case"));
        let optionData = {
            visualMap: {
                show: false,
                min: 80,
                max: 600,
                inRange: {
                    colorLightness: [0, 1],
                }
            },
            series : [
                {
                    type: 'pie',
                    radius: '55%',
                    data:[
                        {value:235, name:'A场'},
                        {value:274, name:'B场'},
                        {value:310, name:'C场'},
                        {value:335, name:'D场'},
                        {value:400, name:'E场'}
                    ],
                    roseType: 'angle',
                    label: {
                        normal: {
                            textStyle: {
                                color:'#fff'
                            }
                        }
                    },
                    labelLine: {
                        normal: {
                            lineStyle: {
                                color:'#fff'
                            }
                        }
                    },
                    itemStyle: {
                        normal: {
                            color: '#3294ff',
                        }
                    }
                }
            ]        
        };
        this.myChart.setOption(optionData)
        this.Init() //方法调用
    }
}
</script>

<style scoped>
    #container_pie,#pie_case{
        width: 100%;
        height: 100%;
    }
</style>
