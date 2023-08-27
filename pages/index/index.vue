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
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				navArr: [],
				newsArr: []
			}
		},
		onLoad() {
			this.getNavData(),
				this.getNewsData()
		},
		methods: {
			clickNav(index, id) {
				this.navIndex = index
				console.log("id: ", id);
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
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: id || this.navIndex,
						num: 3
					},
					success: (res) => {
						// console.log(res);
						this.newsArr = res.data
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
</style>