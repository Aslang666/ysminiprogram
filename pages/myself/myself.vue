<template>
	<!-- login view html start -->
	<view>
		<view>
			<view class="header">
				
			</view>
			<view class="content" v-if="isShow">
				<view>申请获取以下权限</view>
				<text>获得你的公开信息(昵称，头像、地区等)</text>
			<button class="bottom" type="primary" withCredentials="true" @click="getUserProfile">授权登录</button>
			</view>
            <view class="userinfo" v-else>
				<view class="img"><image :src="avatarUrl"></image></view>
                <view class="name">{{nickName}}</view>
            </view>
		</view>
	</view>
	<!-- login view html end -->
</template>
 
<script>
	export default {
		data() {
			return {
				nickName:'',
				avatarUrl:'',
				gender:'',
				isShow:true
			};
		},
		methods: {
			getUserProfile() {
				if(uni.getUserProfile){
					uni.getUserProfile({
						desc: '登录',
						lang:'zh_CN',
						success: (info) => {
							console.log(info.userInfo)
					        //这里取到的是用户的信息，自己安排自己的业务
							this.nickName = info.userInfo.nickName
							this.avatarUrl = info.userInfo.avatarUrl
							this.gender = info.userInfo.gender
							this.isShow = false
							console.log(this.nickName)
							uni.login({
								provider: 'weixin',
								onlyAuthorize:true,
								success: (res) => {
									console.log(res.code)
					                //这里获取的是用户的code，用来换取 openid、unionid、session_key 等信息，再将信息丢给后台自己的登录业务就行了
								}
							})
						},
						fail: (err) => {
							console.log(err);
						}
					})
				}else{
					console.log(err)
				}

			}
		},
		onLoad(options) {
			//默认加载
			// this.getUserProfile();
		}
	};
</script>
 
<style>
	.header {
		margin: 0rpx 0rpx 50rpx 50rpx;
		border-bottom: 1px solid #ccc;
		text-align: center;
		width: 650rpx;
		height: 100rpx;
		line-height: 450rpx;
	}
 
	.header image {
		width: 200rpx;
		height: 200rpx;
	}
 
	.content {
		margin-left: 50rpx;
		margin-bottom: 90rpx;
	}
 
	.content text {
		display: block;
		color: #9d9d9d;
		margin-top: 40rpx;
	}
 
	.bottom {
		border-radius: 80rpx;
		margin: 70rpx 50rpx;
		font-size: 35rpx;
	}
</style>
