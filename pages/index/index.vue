<template>
	<view class="home">
		<scroll-view scroll-x class="navscroll" show-scrollbar="false">
			<view class="item" v-for="(item,index) in 10" :key="index">国内</view>

		</scroll-view>
		<view class="content">
			<view class="row"  v-for="(item,index) in 10" :key="index">
				<NewsBox ></NewsBox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	.navscroll {
		height: 100rpx;
		background-color: #f7f8fa;
		white-space: nowrap;

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
		}
	}

	.content {
		padding: 30rpx;
		.row {
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}
</style>