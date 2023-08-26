<template>
	<view class="home">
		<scroll-view scroll-x class="navscroll" show-scrollbar="false">
			<view class="item" :class="{active:index == navIndex}" v-for="(item,index) in 10" :key="index"
				@click="clickNav(index)">国内</view>

		</scroll-view>
		<view class="content">
			<view class="row" v-for="(item,index) in 10" :key="index" @click="goDetail">
				<NewsBox></NewsBox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0
			}
		},
		onLoad() {

		},
		methods: {
			clickNav(index) {
				this.navIndex = index
			},
			goDetail(){
				uni.navigateTo({
					url:"/pages/detail/detail"
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
</style>