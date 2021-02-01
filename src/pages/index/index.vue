<template>
	<view class="content">
		<view>
			<button open-type="getUserInfo" withCredentials="true" @click='getUserInfo'>登录</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				code: '',
				userInfo: {}
			}
		},
		onLoad() {
			this.getUserInfo()
		},
		methods: {

			getUserInfo() {
				console.log(1111)
				const that  = this
				uni.login({
				provider: 'weixin',
				success: (res) => {
					if (res.errMsg == "login:ok") {
						console.log(res)
						that.code = res.code;
						uni.getUserInfo({
                    success: (res) => {
                        that.userInfo = res.userInfo;
                        console.log(that.userInfo);
                    },
                    fail: () => {
                        console.log("未授权");
                    }
                })
					} else {
						uni.showToast({
							title: '系统异常，请联系管理员!'
						})
					}
				}
			})
				
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin: 200rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
