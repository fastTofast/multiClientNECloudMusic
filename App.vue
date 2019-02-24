<script>
	export default {
		onLaunch: function () {
			console.log('App Launch')
		},
		onShow: function () {
			console.log('App Show')
		},
		onHide: function () {
			console.log('App Hide')
		}
	}
</script>

<style>
	@import "./static/font/iconfont.css";
	page {
		overflow: hidden;
	}
	/*每个页面公共css */
	.top-bar-area {
		display: flex;
		justify-content: center;
		text-align: center;
	}
	.top-nav-bar{
		display: inline-block;
		width: 100upx;
	}
	.index-top-bar {
		height: 40upx;
		width: 40upx;
		border-radius: 4upx;
		margin-top: 10upx;
	}
	.uni-scroll-view::-webkit-scrollbar {
		display: none;
	}
	.hot-swiper .uni-swiper-wrapper {
		border-radius: 8upx !important;
	}
</style>
