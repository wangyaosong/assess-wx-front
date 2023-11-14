<template>
	<view class="v1" style="height:auto">

		<view class="v2">
			<view class="dltext"
				style="width: 232rpx; height: 92rpx; display: block; box-sizing: border-box; left: 0rpx; top: -2rpx">
				登录
			</view>
			<view class="phoneCs">
				<input placeholder="请输入账号" v-model="username" type="content" />
			</view>
			<view class="passwordCs">
				<input placeholder="请输入密码" v-model="password" type="password" />
			</view>
			<view>
				<button class="denglu" type="primary" @click="goadmin()">登录</button>
			</view>

		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				username: '',
				password: '',
				clientHeight: ''
			}
		},
		methods: {
			goadmin() {
				let flag = false //表示账户是否存在,false为初始值
				if (this.username == '' || this.password == '') {
					wx.showToast({
						icon: 'none',
						title: '账号或密码不能为空',
					})
					return;
				}
				//传入数据到后端，进行登录
				uni.request({
					url: getApp().globalData.position + 'Xcxuser/userlogin',
					header: {
						"Content-Type": "application/x-www-form-urlencoded"
					},
					method: 'POST',
					dataType: 'json',
					data: {
						username: this.username,
						password: this.password
					},
					success: res => { //如果获取到服务器
						// console.log(res.data)
						if (res.data == 1) {
							uni.showToast({
								title: '账号不存在',
								icon: "none",
							})
							return
						} else if (res.data == 2) {
							uni.showToast({
								title: '密码错误',
								icon: "none",
							})
							return
						} else if (res.data == 3) {
							uni.showToast({
								title: '账号已失效',
								icon: "none",
							})
							return
						} else {
							//将账号信息作为全局变量
							getApp().globalData.username = res.data[0].username
							uni.setStorageSync('username', res.data[0].username)
							uni.reLaunch({ //跳转到主页，并携带账号参数
								url: '../../pages/saoma/saoma?username=' +
									res.data[0].username
							})
							//存入登录变量
						}
					},
					fail: res => {
						//将账号信息作为全局变量
						getApp().globalData.username = 'zhangsan'
						uni.setStorageSync('username', 'zhangsan')
						uni.reLaunch({ //跳转到主页，并携带账号参数
							url: '../../pages/saoma/saoma?username=zhangsan',
						})
					}
				})

			},
		},

	}
</script>

<style>
	/* pages/login/login.wxss */
	/* 最大的父元素 */
	.v1 {
		display: block;
		position: absolute;
		width: 100%;
		background-color: rgb(250, 248, 248);
	}

	/* 白色区域 */
	.v1 .v2 {
		position: relative;
		margin-top: 150rpx;
		left: 100rpx;
		width: 545rpx;
		height: 600rpx;
		background-color: rgb(250, 248, 248);
		border-radius: 50rpx;
	}

	/* 白色区域内的登录文本 */
	.v1 .v2 .dltext {
		margin-top: 50rpx;
		position: absolute;
		margin-left: 50rpx;
		width: 150rpx;
		height: 100rpx;
		font-size: 60rpx;
		font-family: Helvetica;
		color: #000000;
		line-height: 100rpx;
		letter-spacing: 2rpx;
	}

	/* 手机图片+输入框+下划线的父容器view */
	.v1 .v2 .phoneCs {
		margin-top: 200rpx;
		margin-left: 25rpx;
		position: absolute;
		display: flex;
		width: 480rpx;
		height: 90rpx;
		background-color: white;

	}

	/* 手机图标 */
	.v1 .v2 .phoneCs .ph {
		margin-top: 5rpx;
		margin-left: 30rpx;
		width: 55rpx;
		height: 55rpx;
	}

	/* 手机号输入框 */
	.v1 .v2 .phoneCs input {
		width: 400rpx;
		font-size: 30rpx;
		margin-top: 25rpx;
		margin-left: 30rpx;
	}

	/* 密码图标+输入框+小眼睛图标+下划线父容器view */
	.v1 .v2 .passwordCs {
		margin-top: 350rpx;
		margin-left: 25rpx;
		position: absolute;
		display: flex;
		width: 480rpx;
		height: 90rpx;
		background-color: white;

	}

	/* 密码图标 */
	.v1 .v2 .passwordCs .ps {
		margin-top: 5rpx;
		margin-left: 30rpx;
		width: 55rpx;
		height: 55rpx;
	}

	/* 眼睛 图标*/
	.v1 .v2 .passwordCs .eye {
		margin-top: 5rpx;
		margin-left: 65rpx;
		width: 55rpx;
		height: 55rpx;
	}

	/* 密码输入框 */
	.v1 .v2 .passwordCs input {
		width: 400rpx;
		font-size: 30rpx;
		margin-top: 25rpx;
		margin-left: 30rpx;
	}

	/* 登录按钮容器view */
	.v1 .v2 .denglu {
		width: 480rpx;
		height: 80rpx;
		position: absolute;
		margin-top: 515rpx;
		margin-left: 25rpx;

	}

	/* 登录按钮 */
	.v1 .v2 .denglu button {
		padding: 0rpx;
		line-height: 70rpx;
		font-size: 30rpx;
		width: 100%;
		height: 100%;
		border-radius: 5rpx;
	}
</style>