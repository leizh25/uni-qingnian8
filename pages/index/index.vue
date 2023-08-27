<template>
	<view class="home">
		<scroll-view scroll-x class="navscroll" show-scrollbar="false">
			<view class="item" :class="{active:index == navIndex}" v-for="(item,index) in navArr" :key="index"
				@click="clickNav(index,item.id)">{{item.classname}}</view>

		</scroll-view>
		<view class="content">
			<view class="row" v-for="(item,index) in newsArr" :key="index" @click="goDetail">
				<NewsBox :item="item"></NewsBox>
			</view>
		</view>
		<view class="noData" v-if="!newsArr.length">
			<image src="../../static/images/nodata.png" mode="widthFix"></image>
		</view>
		<view class="loading" v-if="newsArr.length">
			<view v-if="loading == 1">数据加载中...</view>
			<view v-if="loading == 2">没有更多了</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				navArr: [],
				newsArr: [],
				currentPage: 1,
				allLoaded: false,
				loading:0  //0默认  1 加载中  2没有更多了
			}
		},
		onLoad() {
			this.getNavData(),
				this.getNewsData()
		},
		onReachBottom() {
			console.log("到底了哦");
			this.currentPage++
			this.allLoaded || this.getNewsData()
		},
		methods: {
			clickNav(index, id) {
				this.navIndex = index
				// console.log("id: ", id);
				this.newsArr = []
				this.currentPage = 1
				this.allLoaded = false
				this.getNewsData(id)
			},
			goDetail() {
				uni.navigateTo({
					url: "/pages/detail/detail"
				})
			},
			//获取导航列表数据
			getNavData() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/navlist.php",
					success: res => {
						// console.log(res);
						this.navArr = res.data
					}
				})
			},
			//获取新闻列表
			getNewsData(id) {
				this.loading = 1
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: id || this.navIndex,
						num: 10,
						page: this.currentPage
					},
					success: (res) => {
						// console.log(res);
						this.loading = 0
						if (res.data.length == 0) {
							this.allLoaded = true
							this.loading = 2
						}
						this.newsArr = this.newsArr.concat(res.data)
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.navscroll {
		height: 100rpx;
		background-color: #f7f8fa;
		white-space: nowrap;
		position: fixed;
		top: var(--window-top);
		left: 0;
		z-index: 10;

		/* 解决小程序和app滚动条的问题 */
		/* #ifdef MP-WEIXIN || APP-PLUS */
		::-webkit-scrollbar {
			display: none;
			width: 0 !important;
			height: 0 !important;
			-webkit-appearance: none;
			background: transparent;
			color: transparent;
		}

		/* #endif */

		.item {
			font-size: 40rpx;
			display: inline-block;
			line-height: 100rpx;
			padding: 0 30rpx;
			color: #333;

			&.active {
				color: #31C27F;
			}
		}
	}

	.content {
		padding: 30rpx;
		padding-top: 130rpx;

		.row {
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}

	.noData {
		text-align: center;

		image {
			width: 360rpx;

		}
	}

	.loading {
		text-align: center;
		font-size: 26rpx;
		color: #888;
		line-height: 2em;
		
	}
</style>