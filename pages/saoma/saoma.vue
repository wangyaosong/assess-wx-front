<template>
	<view class="v1" style="height:auto">

		<view class="v2">
			<view>
				<button class="saoma" type="primary" @click="saoma()">扫码</button>
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
			saoma() {
				//调用scanCode实现扫码功能
				uni.scanCode({
					//是否只能从相机扫码,不能从相册扫码
					onlyFromCamera: false,
					//规定扫码类型  字节跳动小程序不支持此参数
					// barcode就是一维码(条形码)  qrcode就是(er)维码 
					// datamatrix就是Data Matrix码   pdf417就是PDF417条码
					scanType: ['barCode'],
					// 是否启动自动识别字符编码功能
					autoDecodeCharset: false,
					// 是否开启自动放大功能  仅 App-Android (3.5.4+) 支持
					autoZoom: false,
					// 是否支持手动输入条形码  仅飞书小程序（V3.14.0）支持
					barCodeInput: false,
					success: function(res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				})
			}

		}
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
	.v1 .v2 .saoma {
		width: 480rpx;
		height: 80rpx;
		position: absolute;
		margin-top: 515rpx;
		margin-left: 25rpx;

	}

	/* 登录按钮 */
	.v1 .v2 .saoma button {
		padding: 0rpx;
		line-height: 70rpx;
		font-size: 30rpx;
		width: 100%;
		height: 100%;
		border-radius: 5rpx;
	}
</style>