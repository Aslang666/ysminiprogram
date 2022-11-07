<template>
	<view class="top">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="scroll-area">
			<!-- 横向导航栏 -->
			<scroll-view class="scroll-X" scroll-x="true" >
				<view class="scroll-x">
					<view 
					:class="active===index?'active-x':''" 
					v-for="(item,index) in xTabList" :key="index"
					@click="ontabtap(index)"
					>{{item.name}}</view>					
				</view>
				<!-- 销售or销售额 -->
				<u-subsection 
				fontSize="15px"
				inactiveColor="#4fadff"
				:list="list" 
				:current=current 
				mode="subsection" 
				@change="sectionChange"
				></u-subsection>
				<!-- 竖向导航栏 -->
			</scroll-view>

		</view>
		<view class="area-select">
			<view class="selected-area" @click="showDrawer">
				{{areas[active2].name}}>
			<uni-drawer style="height: 50%; position: fixed; top: 20%; opacity: 1;" ref="showLeft" mode="left" :mask-click="true">
				<scroll-view  scroll-y="true">
					<view @click="selectarea(index)" :class="active2===index ? 'drawer-active':'drawer'" v-for="(item,index) in areas" :key="index" >{{ item.name }}</view>
					<button @click="closeDrawer()" type="primary">选择</button>
				</scroll-view>
			</uni-drawer>
			</view>
			<view class="area-count">
				<ul>
					<li>
						<text class="li-text">0</text>
						<view class="sales-num">
							<text style="color:#999;">
								今日
							</text>
						</view>
					</li>
					<li>
						<text class="li-text">0</text>
						<view class="sales-num">
							<text style="color:#999;">
								昨日
							</text>
						</view>
					</li>
				</ul>
			</view>
		</view>
		<view class="content">
			<scroll-view class="scroll-Y" scroll-y="true" >
				<view class="scroll-y">
					<view 
					:class="active1===index?'active-y':''" 
					v-for="(item,index) in yTabList" 
					:key="index"
					@click="ontabtapy(index)">
						{{item.name}}
					</view>				
				</view>
			</scroll-view>
			
			<!-- 1234 -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				xTabList:[{
					id: "platform01",
					name: 'ASIN',
				},{
					id:"platform02",
					name: '父ASIN'
				}],
				yTabList:[{
					id:0,
					name:'YS-US'
				},{
					id:1,
					name:'PH-US'
				},{
					id:2,
					name:'GH-US'
				},{
					id:3,
					name:'ZHL-US'
				}],
				list:['销售','销售额'],
				areas:[{
					id:0,
					name:'北美'
				},{
					id:1,
					name:'欧洲'
				},{
					id:2,
					name:'非洲'
				}],
				area:0,
				active:0,
				active1:0,
				current:0,
				active2:0
			}
		},
		onLoad() {

		},
		methods: {
			ontabtap(index){
				this.active = index
			},
			ontabtapy(index){
				this.active1 = index
				console.log(this.active1)
			},
			sectionChange(index){
				this.current = index
			},
			showDrawer(){
				this.$refs.showLeft.open();
			},
			selectarea(index){
				this.active2 = index
				console.log(this.active2)
			},
			closeDrawer() {
				this.$refs.showLeft.close();
			}

		}
	}
</script>

<style lang="less">
	.scroll-X{
		border-radius: 20rpx;
		border-top: solid 1px #eee;
		border-bottom: solid 1px #eee;
		.scroll-x{
			margin: 0 50rpx;
			padding: 0 15rpx;
			view{
				margin: 10rpx 65rpx ;
				padding: 10rpx 15rpx;
				font-size: 15px;
				background-color: #ffffff;
				border: solid 1px #4fadff;
				border-radius: 45rpx;
				color: #4fadff;
				display: inline-block;
				width: 150rpx;
				line-height: 70rpx;
				text-align: center;
			}
			.active-x{
				font-size: 15px;
				background-image: linear-gradient(to right,#2b80f8, #52bdff);
				box-shadow:  2rpx 2rpx 10rpx 1rpx rgba(43, 128, 248, 0.5);
				background-color: #4da6f8;
				border-radius: 45rpx;
				color: #FFFFFF;
				display: inline-block;
				width: 152rpx;
				line-height: 72rpx;
				text-align: center;
			}			
		}
	}
	.scroll-Y{
		.scroll-y{
			// margin-top: 10rpx;
			// border-top: solid 1px #eee;
			border-bottom: solid 1px #eee;
			view{
				font-size: 16px;
				background-color: #ffffff;
				border-top: solid 1px #eee;
				border-right: solid 1px #eee;
				color: #4fadff;
				height: 100rpx;
				width: 150rpx;
				line-height: 100rpx;
				text-align: center;
			}
			.active-y{
				font-size: 16px;
				background-image: linear-gradient(to right, #52bdff,#2b80f8);
				box-shadow:  2rpx 2rpx 10rpx 1rpx rgba(43, 128, 248, 0.5);
				background-color: #4da6f8;
				border-radius: 5rpx;
				color: #FFFFFF;
				width: 100%;
				line-height: 100rpx;
				text-align: center;
			}
		}
	}
	.area-select{
		display: flex;
		white-space: nowrap;
		border-bottom: solid 1px #eee;
		.area-count{
			ul{
				// padding: 10rpx 0;
				display: flex;
				list-style: none;
				li{
					float: left;
					width: 50%;
					text-align: center;
					text{
						// width: 50rpx;
					}
				}
			}
		}
	}
	.drawer{
		// background-image: linear-gradient(to right, #52bdff,#2b80f8);
		border: solid 1px #4fadff;
		// border-radius: 45rpx;
		color: #4fadff;
		margin: 20rpx 110rpx;
		width: 220rpx;
		height: 70rpx;
		line-height: 70rpx;
		text-align: center;
	}
	.drawer-active{
		background-image: linear-gradient(to right, #52bdff,#2b80f8);
		color: white;
		margin: 20rpx 110rpx;
		width: 220rpx;
		height: 70rpx;
		line-height: 70rpx;
		text-align: center;
	}
	.selected-area{
		font-size: 16px;
		font-weight: bolder;
		// background-image: linear-gradient(to right, #52bdff,#2b80f8);
		// box-shadow:  2rpx 2rpx 10rpx 1rpx rgba(43, 128, 248, 0.5);
		// border-top: solid 1px #eee;
		border-right: solid 1px #eee;
		background-color: white;
		border-radius: 5rpx;
		color: #4fadff;
		width: 150rpx;
		line-height: 100rpx;
		text-align: center;
	}
	.content{
		display: flex;
		float: left;
		
	}
</style>
