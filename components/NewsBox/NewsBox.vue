<template>
	<view class="newsBox">
		<view class="pic">
			<image src="../../static/images/0.jpg" mode="aspectFill"></image>
		</view>
		<view class="text">
			<view class="title">默认的新闻标题默认的新闻标题默认的新闻标题默认</view>
			<view class="info">
				<text>作者名称</text>
				<text>998浏览</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "NewsBox",
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.newsBox {
		display: flex;

		.pic {
			width: 230rpx;
			height: 160rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.text {
			flex: 1;
			padding-left: 20rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.title {
				font-size: 38rpx;
				color: #333;
				overflow: hidden;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-line-clamp: 2;
				-webkit-box-orient: vertical;
			}

			.info {
				font-size: 26rpx;
				color: #999;

				text {
					padding-right: 30rpx;
				}
			}
		}
	}
</style>