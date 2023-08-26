<template>
	<view class="newsBox">
		<view class="pic">
			<image :src="item.picurl" mode="aspectFill"></image>
		</view>
		<view class="text">
			<view class="title">{{item.title}}</view>
			<view class="info" v-if="!item.lookTime">
				<text>{{item.author}}</text>
				<text>{{item.hits}}浏览</text>
			</view>
			<view class="info" v-else>
				<text>浏览时间: {{item.lookTime}}</text>
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
		},
		props: {
			item: {
				type: Object,
				default: () => {
					return {
						title: "组件内默认标题",
						author: "张三",
						hits: 998,
						picurl: "../../static/images/nopic.jpg",
						// lookTime:"2023-08-26 12:34:56"
					}
				}
			}
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
				font-size: 36rpx;
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