<template>
	<view class="top-container">
		<image class="top-bg" src="../../static/home_top_bg.jpg"></image>
		<view class="date-text">
			{{date | time}}
		</view>
		<view class="sales-box">
			<ul class="sales-ul">
				<li class="sales-li">
					<text class="li-text">销量</text>
					<view class="sales-num">
						<text style="color:#edff20; font-size:65rpx">
							{{sales}}
						</text>
					</view>
					<view class="compare">
						<text>较昨日</text>
						<text style="color:pink">
							{{sales_difference | compare}}
						</text>
					</view>
				</li>
				<li class="sales-li">
					<text class="li-text">销售额</text>
					<view class="sales-num">
						<text style="color:#edff20 ; font-size:65rpx">
							{{sales_amount | dollars}}
						</text>
					</view>
					<view class="compare">
						<text>较昨日</text>
						<text style="color:pink">
							{{sales_amount_difference | compare}}
						</text>
					</view>
				</li>
			</ul>
		</view>
		<view class="charts">
			<uCharts></uCharts>
			<!-- <view class="title" style="display: flex;float: left; align-items: flex-end">
			<image style="width: 56rpx; height: 56rpx; padding: 0 8rpx;" src="../../static/sales-report_fill_active.png"></image>
			<u--text  bold size="40rpx" text="近七日数据"></u--text>
			<view style="font-size: 26rpx; color: #909399;padding-left: 8rpx;">
				根据每个站点当地日期进行汇总
			</view> -->
			<!-- </view> -->
			<!-- <view class="wrapper">
				<scroll-view class="scroll" scroll-x="true" scroll-with-animation="true">
					<qiun-data-charts inScrollView :canvas2d='true' canvasId='canvans1' class="u-chart" type="area" :chartData="chartData1" :opts="opts" background="none" />
					<qiun-data-charts inScrollView :canvas2d='true' canvasId='canvans2' class="u-chart" type="line" :chartData="chartData2" :opts="opts" background="none" />
				</scroll-view>
			</view> -->
		</view>
	</view>
</template>

<script >
	import uCharts from '../../components/ucharts.vue'
	export default {
		components:{
			uCharts
		},
		data() {
			return {
				date:'',
				sales:'2550',
				sales_amount:'20000',
				sales_difference:'200',
				sales_amount_difference:'11990',
				week:'10.23',
				all:'160',
				chartData1:{
				},
				chartData2:{
				},
				opts:{
					color:["#599ef5","#0dc59f"],
					padding: [20,10,0,10],
					legend: {
											show: true,
											position: 'bottom',
											float: 'center',
											padding: 0,
											lineHeight: 5,
											margin: 6,
										},
					yAxis: {
							calibration: true,
					        gridType: "dash",
					        dashLength: 8,
							showTitle: true,
							splitNumber: 5 ,
							data:[{
								position: 'left',
								title: '销量',
								titleFontSize: 15,
								format: (val) => {
									return '$'+val
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
		onLoad() {
			// this.getServerData()
		},
		methods: {
			// getServerData() {
			//       //模拟从服务器获取数据时的延时
			//     setTimeout(() => {
			//         let res = {
			// 			index:0,//当前点位的索引值
			//             categories: [this.week,"10.30","10.31","11.01","11.02","11.03","11.04"],
			//             series: [
			//               {
			//                 name: "总销量",
			//                 data: [this.all,76,81,59,120,22,33],
			// 				show:true,
			//               },
			// 			  {
			// 			    name: "亚马逊",
			// 			    data: [35,36,51,33,50],
			// 				show:false
			// 			  },
			// 			  {
			// 			    name: "沃尔玛",
			// 			    data: [20,26,31,33,40],
			// 				show:false
			// 			  },
			//               {
			//                 name: "亚马逊",
			//                 data: [16,27,21,24,6],
			// 				show:false
			//               }
			//             ]
			//           };
			//         this.chartData1 = JSON.parse(JSON.stringify(res));
			//       }, 10);
			// 	setTimeout(() => {
			// 	    let aa = {
			// 	        categories: [this.week,"10.30","10.31","11.01","11.02","11.03","11.04"],
			// 	        series: [
			// 	            {
			// 					name: "总销售额",
			// 					data: [30000,76,81,59,120,22,33],
			// 	  							show:true,
			// 	            },
			// 	  			{
			// 	  				name: "亚马逊",
			// 	  				data: [35,36,51,33,50],
			// 	  				show:false
			// 	  			},
			// 	  			{
			// 	  				name: "沃玛",
			// 	  				data: [20,26,31,33,40],
			// 	  				show:false
			// 	  			},
			// 	          {
			// 	            name: "亚马逊",
			// 	            data: [16,27,21,24,6],
			// 	  			show:false
			// 	          }
			// 	        ]
			// 	      };
			// 	  	this.chartData2 = JSON.parse(JSON.stringify(aa));
			// 	  }, 10);}
		},
		filters:{
			time:function(date){
				var date = new Date()
				var MM = date.getMonth()+1
				MM = MM<10?'0'+MM : MM
				var DD = date.getDate()
				DD = DD<10?'0'+DD : DD
				return `${MM}月${DD}日 `
			},
			dollars:function(num){
				return `$${num}`
			},
			compare:function(difference){
				var difference = difference > 0 ? '+'+ difference : '-' + difference
				return difference
			}
		}
	}
</script>

<style lang="less" scoped>
	.top-container{
		.top-bg{
			width: 100%;
			height: 400rpx;
			position: absolute;
			z-index: -1;
			opacity: 0.8;
			border-radius: 30rpx;
		}
		.sales-box{
			color: white;
			ul{
				padding: 10px;
			    display: flex;
				list-style: none;
				.sales-li{
					float: left;
					width: 50%;
					text-align: center;
					padding: 6% 0;
					.li-text{
						// border: solid 1px;
						// color: #aaff7f;
						font-size: 40rpx;
						font-weight: normal;
					}
				}
			}
		}
		.charts{
			margin:50rpx 0rpx;
			// padding: 0 20rpx;
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
		.date-text{
			padding-top: 20rpx;
			font-size: 38rpx;
			text-align: center;
			color: white;
		}
		// .scroll{
		// 	line-height: 700rpx;
		// }
	}
</style>
