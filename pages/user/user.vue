<template>
	<view class="user">
		<view class="top">
			<image src="../../static/images/history.png" mode=""></image>
			<view class="text">浏览历史</view>
		</view>
		<view class="content">
			<view class="row" v-for="(item,index) in listArr" :key="index">
				<NewsBox :item="item" @click.native="goDetail(item)"></NewsBox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				listArr: []
			};
		},
		onLoad() {
			this.getData()
		},
		methods: {
			goDetail(item) {
				uni.navigateTo({
					url: `/pages/detail/detail?cid-${item.classid}&id=${item.id}`,
				})
			},
			//获取缓存浏览记录
			getData() {
				this.listArr = uni.getStorageSync("historyArr") || []
				console.log(this.listArr);
			}
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