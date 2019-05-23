<template>
    <div id="container_line">
        <div id="line_case"></div>
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
        this.myChart = echarts.init(document.getElementById("line_case"));
        let data = [["06-05",116],["06-06",129],["06-07",135],["06-08",86],["06-09",73],["06-10",85],["06-11",73],["06-12",68],["06-13",92],["06-14",130],["06-15",245],["06-16",139],["06-17",115],["06-18",111],["06-19",309],["06-20",206],["06-21",137],["06-22",128],["06-23",85],["06-24",94],["06-25",71],["06-26",106],["06-27",84],["06-28",93],["06-29",85],["06-30",73],["07-01",83],["07-02",125],["07-03",107],["07-04",82],["07-05",44],["07-06",72],["07-07",106],["07-08",107],["07-09",66],["07-10",91],["07-11",92],["07-12",113],["07-13",107],["07-14",131],["07-15",111],["07-16",64],["07-17",69],["07-18",88],["07-19",77],["07-20",83],["07-21",111],["07-22",57],["07-23",55],["07-24",60]];
        let dateList = data.map(function (item) {
            return item[0];
        });
        var valueList = data.map(function (item) {
            return item[1];
        });     
        let optionData = {
            tooltip: {
                trigger: 'axis'
            },
            xAxis: [{
                data: dateList,
                axisLine: { //坐标轴颜色
                    lineStyle: {
                        color: "#fff",
                    }
                }
            }],
            yAxis: [{
                splitLine: {show: false},
                axisLine: { //坐标轴颜色
                    lineStyle: {
                        color: "#fff",
                    }
                }
            }],
            grid: {
                left: '15%',
                top:'10%',
                bottom:'15%',
                right:'10%'
            },
            series: [{
                type: 'line',
                showSymbol: false,
                data: valueList,
                color: '#389ffe'
            }]         
        };
        this.myChart.setOption(optionData)
        this.Init() //方法调用
    }
}
</script>

<style scoped>
    #container_line,#line_case{
        width: 100%;
        height: 100%;
    }
</style>
