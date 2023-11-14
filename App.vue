<script>
	export default {
		onLaunch: function() {
			// 展示本地存储能力
			const logs = uni.getStorageSync('logs') || []
			logs.unshift(Date.now())
			uni.setStorageSync('logs', logs)
			// 登录
			const username = uni.getStorageSync('username')
			console.log('全局' + username)
			this.globalData.username = username
			if (username) {
				uni.reLaunch({
					url: './pages/start_production/start_index/start_index?username=' + username,
				})
			}

		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		globalData: {
			position: 'XXX',
			icon: 'XXX',
			username: ''
		}

	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import '@/uni_modules/uni-scss/index.scss';
	/* #ifndef APP-NVUE */
	@import '@/static/customicons.css';

	// 设置整个项目的背景色
	page {
		background-color: #f5f5f5;
	}

	/* #endif */
	.example-info {
		font-size: 14px;
		color: #333;
		padding: 10px;
	}
</style>