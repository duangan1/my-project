<template>
    <!-- <div> -->
         <div style="width:50%;height:500px;left:25%" ref="chart"></div>
    <!-- </div> -->
</template>
<script>
export default{
    data () {
　　    return {};
　  },
    methods: {
    　　initCharts () {
        　　let myChart = this.$echarts.init(this.$refs.chart);
        　　console.log(this.$refs.chart)
        　　// 绘制图表
        　　function randomData() {
                now = new Date(+now + oneDay);//让当前日期加上一天，也就是每次执行这个函数的时候会+1天
                value = value + Math.random() * 21 - 10;//生成一个随机的数值
                return {
                    name: now.toString(),//时间转字符
                    value: [
                        [now.getFullYear(), now.getMonth() + 1, now.getDate()].join('/'),
                        Math.round(value)//随机的值取整
                    ]
                };
            }

            var data = [];
            var now = +new Date(1997, 9, 3);//起始日期 等同于new Date(1997,9,3).getTime()
            //加号是JS中的小技巧，转数值型，例如，var str = "233";var num = +str;
            var oneDay = 24 * 3600 * 1000;//一天的毫秒数
            var value = Math.random() * 1000;//生成一个随机的数值
            for (var i = 0; i < 1000; i++) {
                data.push(randomData());//循环执行randomData,并将结果放入data数组
            }

            var option = {
                title: {
                    text: '动态数据 + 时间坐标轴'
                },
                tooltip: {
                    trigger: 'axis',
                    formatter: function (params) {
                        params = params[0];
                        var date = new Date(params.name);
                        return date.getDate() + '/' + (date.getMonth() + 1) + '/' + date.getFullYear() + ' : ' + params.value[1];
                    },
                    axisPointer: {
                        animation: false
                    }
                },
                xAxis: {
                    type: 'time',
                    splitLine: {
                        show: false
                    }
                },
                yAxis: {
                    type: 'value',
                    boundaryGap: [0, '100%'],
                    splitLine: {
                        show: false
                    }
                },
                series: [{
                    name: '模拟数据',
                    type: 'line',
                    showSymbol: false,
                    hoverAnimation: false,
                    data: data
                }]
            };
            myChart.setOption(option);
            setInterval(function () {
                for (var i = 0; i < 5; i++) {
                    // data.shift();//shift() 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。
                    data.push(randomData());
                }

                myChart.setOption({
                    series: [{
                        data: data
                    }]
                });
            }, 1000);
            
        },
    },
    mounted () {
　　    this.initCharts();
　  }
}
</script>