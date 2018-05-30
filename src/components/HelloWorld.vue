<template>
 <div class="gene">
   <div class="company">
     <div class="title">echarts-sdemo</div>
     <div id="myChart" style="width:100%;height:500px;"></div>
   </div>
   
 </div>
</template>

<script>
import echarts from 'echarts';
let $echarts = echarts; 
  export default {
    data() {
      return {
    	exps:[],
		students:[],
		da:[]
      }
    },
    
    computed: {
     
    },
    
    created(){

    },
    
    mounted(){
      this.drawLine();
//    console.log(this.processWith);
    },
    
    methods:{
      drawLine: function() {
      	console.log(this.da);
        // 基于准备好的dom，初始化echarts实例
        let myChart = $echarts.init(document.getElementById('myChart'))
				//月份  x轴				
        for (var e=1;e<13;e++) {
        	this.exps.push(e)
        }
				//风机编号 y轴
				for (var s=1;s<34;s++){
					this.students.push(s)
				}
				//随机故障数
				for (var i=0;i<33;i++){
					for (var j=0;j<12;j++){
						this.da.push([i,j,Math.floor(Math.random()*200)])
						// i j ,Math.floor(Math.random()*100)
						//item[1]表示y轴    【0】表示 x轴   【2】表示数量
					}
				}

				this.da = this.da.map(function(item) {
					return [item[1], item[0], item[2] || '-'];
					//item[1]表示y轴     【0】表示 x轴    【2】表示数量
				});
				//绘制图表
				myChart.setOption({
					tooltip: {
						position: 'top'
					},
					animation: false,
					grid: {
						height: '80%',
						left:'25%',
						y: '6%',
						width:'50%'
					},
					xAxis: {
						type: 'category',
						name: '月',
						data:this.exps,
						axisTick: {
							show:false,
							length:5
						},
						splitArea: {
							show: true
						}
					},
					yAxis: {
						type: 'category',
						name: '风机编号',
						data:this.students,
						axisTick: {
							show:false,
							length:5
						},
						splitArea: {
							show: true
						}
					},
					visualMap: [{
						type:'piecewise',
						min: 0,
						max: 200,
						splitNumber:4,
						name:'故障次数',
						calculable: true,
						orient: 'vertical',
						left: '80%',
						bottom: '20%',
						itemHeight:'50',
						inRange: {
											color: ['#00ff00','#ffff00','#ff0000']
									}
					}],
					series: [{
						name: '风机故障（次）',
						type: 'heatmap',
						data:this.da,	
						label: {
							normal: {
								show: false
							}
						}, 
						itemStyle: {
							emphasis: {
								shadowBlur: 10,
								shadowColor: 'rgba(0, 0, 0, 0.5)'
							}
						}
					}]
				});
      },
    },
    
    components: {

    }
  }
</script>

<style scoped>
.company{
	width: 100%;
}
</style>	