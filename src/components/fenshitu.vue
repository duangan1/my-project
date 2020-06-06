<template>
    <div class="fenshitu">
        
        <div style="width:25%;height:300px;left:0%" ref="chart"></div>
        <div class="input">
            <input class="div-inline" v-model="code" placeholder="input code">
            <p class="div-inline" id='name'></p>
        </div>
        <!-- <p>Message is: {{ code }}</p> -->
    </div>
</template>

<script>
import {
	bgColor,
	upColor,
	downColor,
	addTimeStr,
	getNextTime,
	time_arr,
	get_m_data,
	initMOption,
	ratioCalculate,
	splitData
} from './k-line'
// import {mdata} from './tmpData'
// import echarts from 'echarts'
export default{
    data () {
　　    return {
        code:'sh000001',
    };
　  },
    methods: {
    　　initCharts () {
            // console.log(fenshi.bgColor)
            // console.log(fenshi.addTimeStr)
        　　let myChart = this.$echarts.init(this.$refs.chart);
            var mdata
        // 　　console.log(this.$refs.chart)
        　　// 绘制图表
            $.ajaxSetup({async:false});
            // $.post("http://localhost:5500/data_api",{code: '002049'},function(json){
            // // $.get("http://localhost:5500/data_api",function(data,status){
            //     // alert("Data: " + data + "\nStatus: " + status);
            //     // alert(json.name)
            //     mdata=json
            //     document.getElementById('name').innerHTML=json.name
            // });
            $.ajax({
                type:"post",
                url:"http://localhost:5500/data_api",
                data:JSON.stringify({ //【这里填写是传给服务端的数据 可传可不传 数据必须是json格式】
                    "code":this.code,
                }),
                dataType:'json',  //【这里要小心啊，不要用jsonp，一定是json】
                crossDomain: true,  //【这个很重要，一定要加】
                success:function(result){
                    // console.log(result);
                    mdata=result
                    document.getElementById('name').innerHTML=result.name
                },
                error:function(result){
                    document.getElementById('name').innerHTML='input error'
                    console.log(result);
                }
            });

            console.log(mdata)
            var option = initMOption(mdata, 'hs')
            myChart.setOption(option);
        },
    },
    mounted () {
        this.initCharts();
        this.timer=setInterval(this.initCharts, 5000);
　  },
    beforeDestroy() {
      clearInterval(this.timer);
    }
}
</script>

<style scoped>
/* h4 { 
  position: absolute;
  left:0%;
  top:0%
} */
.div-inline{ display:inline} 
</style>