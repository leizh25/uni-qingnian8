<template>
	<view class="user">
		<view class="top">
			<image src="../../static/images/history.png" mode=""></image>
			<view class="text">浏览历史</view>
		</view>
		<view class="content">
			<view class="row" v-for="(item,index) in 10" :key="index">
				<NewsBox></NewsBox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.user {
		.top {
			padding: 50rpx 0;
			background-color: #f8f8f8;
			color: #666;
			text-align: center;
			// display: flex;
			// flex-direction: column;
			// align-items: center;

			image {
				width: 150rpx;
				height: 150rpx;
			}

			.text {
				font-size: 38rpx;
				padding-top: 20rpx;
			}
		}
		.content {
			padding: 30rpx;
		
			.row {
				border-bottom: 1px dotted #efefef;
				padding: 20rpx 0;
			}
		}
	}
</style>