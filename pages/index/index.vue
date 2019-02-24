<template>
	<view class="content">
		<scroll-view scroll-x class="top-bar-area">
			<view class="top-nav-bar" @click="tabIndex=0">
				<i class="iconfont icon-z" />
				<!-- <image class="index-top-bar" src="../../static/images/logo.png"></image> -->
			</view>
			<view class="top-nav-bar" @click="tabIndex=1">
				<i class="iconfont icon-yuandian" />
				<!-- <image class="index-top-bar" src="../../static/images/logo.png"></image> -->
			</view>
			<view class="top-nav-bar" @click="tabIndex=2">
				<i class="iconfont icon-shipin" />
				<!-- <image class="index-top-bar" src="../../static/images/logo.png"></image> -->
			</view>
		</scroll-view>
		<swiper :current="tabIndex" class="swiper-box">
			<swiper-item item-id="0">
				<Recommond></Recommond>
			</swiper-item>
		</swiper>
		<!-- <view><button type="primary" @click="num++">+</button></view> -->
	</view>
</template>
<script>
	import Recommond from '../../components/recommond.vue';
	export default {
		data() {
			return {
				num: 0,
				tabIndex: 0
			};
		},
		components: {
			Recommond
		},
		onLoad() {

		},
		created() {
			console.log('=====index created==========')
		},
		methods: {
			toPage(index) {
				let urls = ['/pages/index/index', '/pages/user/user', '/pages/index/index'];
				uni.navigateTo({
					url: urls[index]
				});
			}
		}
	};
</script>

<style scoped>
	.top-bar-area {
		background-color: #504a4a;
	}

	.top-nav-bar {
		width: 50px;
		height: 30px;
		display: inline-block;
		line-height: 30px;
	}

	.content {
		text-align: center;
		height: 100%;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}

	.swiper-box {
		height: 1186upx;
	}
</style>
