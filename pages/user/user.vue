<template>
	<view class="user">
		<view class="top">
			<image src="../../static/images/history.png" mode=""></image>
			<view class="text">浏览历史</view>
			<view class="btn_box">
				<button class="btn" size="mini" @click="clearHis">清除记录</button>
			</view>
		</view>
		
		<view class="content">
			<view class="row" v-for="(item,index) in listArr" :key="index">
				<NewsBox :item="item" @click.native="goDetail(item)"></NewsBox>
			</view>
		</view>
		<view class="nohis" v-if="!listArr.length">
			<image src="../../static/images/nodata.png" mode="widthFix"></image>
			<view class="text">暂无浏览记录</view>
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
		onShow() {
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
			},
			//清除历史记录
			clearHis(){
				uni.removeStorageSync("historyArr")
				this.getData()
			}
			
		}
	}
</script>

<style lang="scss">
	.user {
		.top {
			padding: 50rpx 0;
			padding-bottom: 0;
			background-color: #f8f8f8;
			color: #666;
			text-align: center;
			// display: flex;
			// flex-direction: column;
			// align-items: center;
			.btn{
				margin-right: 30rpx;
			}

			image {
				width: 150rpx;
				height: 150rpx;
			}

			.text {
				font-size: 38rpx;
				padding-top: 20rpx;
			}
		}
		.btn_box{
			text-align: right;
		}

		.content {
			padding: 30rpx;

			.row {
				border-bottom: 1px dotted #efefef;
				padding: 20rpx 0;
			}
		}
		.nohis{
			text-align: center;
			image{
				width: 400rpx;
			}
			.text{
				font-size: 26rpx;
				color: #888;
			}
		}
	}
</style>