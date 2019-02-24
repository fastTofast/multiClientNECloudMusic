<template>
	<view class="recommond-com">
		<scroll-view class="top-bar-foo">
			<view :class="['top-bar',tabIndex===0?'active':'']" @click="tabIndex=0"><text>推荐</text></view>
			<view :class="['top-bar',tabIndex===1?'active':'']" @click="tabIndex=1"><text>朋友</text></view>
			<view :class="['top-bar',tabIndex===2?'active':'']" @click="tabIndex=2"><text>电台</text></view>
		</scroll-view>
		<swiper :current="tabIndex" class="recommond-body">
			<swiper-item class="recommond-content">
				<view class="recommond-content-item">
					<scroll-view scroll-y class="scroll-img-foo">
						<view class="bg-gray"></view>
						<swiper class="hot-swiper" :indicator-dots="true" autoplay="true" :interval="3000" :duration="1000">
							<swiper-item v-for="(item, index) in albums" :key="index">
								<view class="swiper-item">
									<image class="scroll-img" :src="item.picUrl" mode="scaleToFill"></image>
								</view>
							</swiper-item>
						</swiper>
						<view style="position: relative;top: -100upx;">
							<view class="func-list">
								<view class="func-block">
									<view class="func-icon"></view><text class="func-text">私人FM</text>
								</view>
								<view class="func-block">
									<view class="func-icon"></view><text class="func-text">每日推荐</text>
								</view>
								<view class="func-block">
									<view class="func-icon"></view><text class="func-text">歌单</text>
								</view>
								<view class="func-block">
									<view class="func-icon"></view><text class="func-text">排行榜</text>
								</view>
							</view>
							<view class="more-song">
								<text>推荐歌单&nbsp;></text>
							</view>
							<view class="song-list">
								<view style="width:230upx;" v-for="(item,index) in recommondSongLsit" :key="index">
									<view>
										<image style="width: 230upx;height: 230upx;border-radius: 8upx;" :src="item.picUrl" mode="scaleToFill"></image>
									</view>
									<text style="font-size: 12px;display: inline-block;">{{item.name}}</text>
								</view>
							</view>
							<view class="more-song">
								<text>最新音乐&nbsp;></text>
							</view>
							<view class="song-list">
								<view style="width:230upx;" v-for="(item,index) in newMusic" :key="index">
									<view>
										<image style="width: 230upx;height: 230upx;border-radius: 8upx;" :src="item.coverImgUrl" mode="scaleToFill"></image>
									</view>
									<text style="font-size: 12px;display: inline-block;">{{item.name}}</text>
								</view>
							</view>
							<view class="more-song">
								<text>推荐电台&nbsp;></text>
							</view>
							<view class="song-list">
								<view style="width:230upx;" v-for="(item,index) in djRecommond" :key="index">
									<view>
										<image style="width: 230upx;height: 230upx;border-radius: 8upx;" :src="item.picUrl" mode="scaleToFill"></image>
									</view>
									<text style="font-size: 12px;display: inline-block;">{{item.name}}</text>
								</view>
							</view>
						</view>
					</scroll-view>
				</view>
			</swiper-item>
			<swiper-item class="recommond-content bg">
				<view class="swiper-item">
					Nothing2222
				</view>
			</swiper-item>
			<swiper-item class="recommond-content bg">
				<view class="swiper-item">
					Nothing33333
				</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabIndex: 0,
				albums: [{
					picUrl: 'http://localhost:8082/#/'
				}],
				newMusic: [],
				djRecommond: [],
				recommondSongLsit: []
			};
		},
		created() {
			console.log('========created=========');
			// url: 'http://localhost:3000/top/album?offset=0&limit=5',
			uni.request({
				url: 'http://localhost:3000/personalized/privatecontent',
				success: res => {
					this.albums = res.data.result.slice(0, 6);
					console.log(this.albums, res.data.result);
				}
			});
			uni.request({
				url: 'http://localhost:3000/personalized',
				success: (res) => {
					this.recommondSongLsit = res.data.result.slice(0, 6)
				}
			})
			uni.request({
					url: 'http://localhost:3000/top/playlist?limit=6&order=new',
					success: (res) => {
						this.newMusic = res.data.playlists
					}
				}),
				uni.request({
					url: 'http://localhost:3000/personalized/djprogram',
					success: (res) => {
						this.djRecommond = res.data.result.slice(0, 6)
					}
				})
		},
		onLoad() {
			console.log('========onLoad=========');
		},
		onShow() {
			console.log('========onShow=========');
		},
		onReady() {
			console.log('=========onReady========');
		},
		methods: {}
	};
</script>

<style lang="less">
	.recommond-com {
		height: 100%;
		
		.recommond-body {
			position: relative;
			margin: auto;
			min-height: calc(100% - 60upx);

			.bg {
				background-color: #ffffff
			}
		}

		.bg-gray {
			background-color: #504a4a;
			height: 160upx;
			width: 100%;
		}

		.top-bar-foo {
			background-color: #504a4a;
			padding: 18upx 0 8upx;
			text-align: center;
			font-size: 13px;
		}

		.top-bar {
			display: inline-block;
			width: 240upx;
			color: #dedede;
		}

		.top-bar.active {
			border-bottom: 1px solid #ffffff;
			color: #ffffff;
		}

		.scroll-img-foo,
		.recommond-content-item {
			height: 100%;
		}

		.func-list {
			margin: 40upx auto;
			display: flex;
			justify-content: center;
			font-size: 12px;
			overflow: hidden;

			.func-block {
				width: 187.5upx;

				.func-icon {
					width: 90upx;
					height: 90upx;
					margin: 10upx auto;
					border-radius: 90upx;
					background-color: aliceblue;
				}
			}
		}

		.hot-swiper {
			height: 300upx;
			width: 720upx;
			margin: auto;
			position: relative;
			top: -160upx;

			.swiper-item,
			.swiper-item .scroll-img {
				height: 300upx;
				width: 100%;
			}
		}

		.more-song {
			text-align: left;
			font-size: 14px;
			margin: 50upx 20upx 6upx;
			overflow: hidden;
		}

		.song-list {
			width: 710upx;
			display: flex;
			flex-wrap: wrap;
			justify-content: space-between;
			margin: auto;
		}
	}
</style>
