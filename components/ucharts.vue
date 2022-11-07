<template>
	<view>
		<view class="charts">
			<view class="title" style="display: flex;float: left; align-items: flex-end">
			<image style="width: 56rpx; height: 56rpx; padding: 0 8rpx;" src="../static/sales-report_fill_active.png"></image>
			<u--text  bold size="40rpx" text="近七日数据"></u--text>
			<view style="font-size: 26rpx; color: #909399;padding-left: 8rpx;">
				根据每个站点当地日期进行汇总
			</view>
			</view>
			<view class="wrapper">
				<scroll-view class="scroll" scroll-x="true" scroll-with-animation="true">
					<qiun-data-charts inScrollView :canvas2d='true' canvasId='canvans1' class="u-chart" type="area" :chartData="chartData1" :opts="opts1" background="none" />
					<qiun-data-charts inScrollView :canvas2d='true' canvasId='canvans2' class="u-chart" type="line" :chartData="chartData2" :opts="opts2" background="none" />
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"ucharts",
		data() {
			return {
				week:'10.23',
				all:'160',
				chartData1:{
				},
				chartData2:{
				},
				opts1:{
					color:["#599ef5","#0dc59f"],
					padding: [20,10,10,10],
					yAxis: {
							calibration: true,
					        gridType: "dash",
					        dashLength: 8,
							showTitle: true,
							splitNumber: 5 ,
							data:[{
								position: 'left',									title: '销量',
								titleFontSize: 15,
								// unit:'',
								format: (val) => {
									return val.toFixed(0)+'元'
								}
							  }]
					},
					xAxis: {
						boundaryGap: "center",
						scrollShow: true,
						scrollAlign: 'right',	 
					},
					extra: {
						area: {
							type: "curve",
							width: 2,
							gradient: false
						},
						line: {
							type: "curve"
						},
						tooltip: {
							bgOpacity: 0.7,
							gridType: 'solid',
						}
					},	
					inScrollView:true
				},
				opts2:{
					color:["#599ef5","#0dc59f"],
					padding: [20,10,10,10],
					yAxis: {
							calibration: true,
					        gridType: "dash",
					        dashLength: 8,
							showTitle: true,
							splitNumber: 5 ,
							data:[{
								position: 'left',									
								title: '销售额',
								titleFontSize: 15,
								format:'yAxisDemo3'
							  }]
					},
					xAxis: {
						boundaryGap: "center",
						scrollShow: true,
						scrollAlign: 'right',	 
					},
					extra: {
						line: {
							type: "curve"
						},
						tooltip: {
							bgOpacity: 0.7,
							gridType: 'solid',
						}
					},	
					inScrollView:true
				},
				canvas2d:{}
			}
		},
		mounted() {
			this.getServerData()
		},
		methods:{
			getServerData() {
			      //模拟从服务器获取数据时的延时
			    setTimeout(() => {
			        let res = {
						index:0,//当前点位的索引值
			            categories: [this.week,"10.30","10.31","11.01","11.02","11.03","11.04"],
			            series: [
			              {
			                name: "总销量",
			                data: [this.all,76,81,59,120,22,33],
							show:true,
			              },
						  {
						    name: "亚马逊",
						    data: [35,36,51,33,50],
							show:false
						  },
						  {
						    name: "沃尔玛",
						    data: [20,26,31,33,40],
							show:false
						  },
			              {
			                name: "亚马逊",
			                data: [16,27,21,24,6],
							show:false
			              }
			            ]
			          };
			        this.chartData1 = JSON.parse(JSON.stringify(res));
			      }, 10);
				setTimeout(() => {
				    let res = {
				        categories: [this.week,"10.30","10.31","11.01","11.02","11.03","11.04"],
				        series: [
				            {
								name: "总销售额",
								data: [30100,29736,21381,30919,27120,32821,22923],
				  							show:true,
				            },
				  			{
				  				name: "亚马逊",
				  				data: [11315,1361,1512,1333,1502],
				  				show:false
				  			},
				  			{
				  				name: "沃玛",
				  				data: [11120,1226,1131,1133,1140],
				  				show:false
				  			},
				          {
				            name: "亚马逊",
				            data: [11116,11127,1121,1024,2016],
				  			show:false
				          }
				        ]
				      };
				  	this.chartData2 = JSON.parse(JSON.stringify(res));
				  }, 10);}
		}
	}
</script>

<style lang="less" scoped>
.charts{
			margin:50rpx 0rpx;
			width: 100%;
		    height: 300px;
			.wrapper{
				white-space: nowrap;
			}
				.u-chart{
				padding-top: 30rpx;
					display: inline-block;
				}
		}
</style>
