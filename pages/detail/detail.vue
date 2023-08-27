<template>
	<view class="detail">
		<view class="title">{{detail.title}}</view>
		<view class="info">
			<view class="author">编辑: {{detail.author}}</view>
			<view class="time">发布日期: {{detail.posttime}}</view>
		</view>
		<view class="content">
			<rich-text :nodes="detail.content"></rich-text>
		</view>
		<view class="description">
			声明:本站的内容均采集于腾讯新闻,如果侵权请联系管理(leizhuzheng@qq.com)进行整改删除,本站进行的内容采集不代表本站及作者观点,若有侵犯请及时联系管理员,谢谢您的支持</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				options: null,
				detail: {}
			};
		},
		onLoad(e) {
			// console.log(e);
			this.options = e
			this.getDetail()
		},
		methods: {
			getDetail() {
				uni.request({
					url: "http://ku.qingnian8.com/dataApi/news/detail.php",
					data: this.options,
					success: (res) => {
						console.log(res);
						this.detail = res.data
					}
				})
			}
		}

	}
</script>

<style lang="scss">
	.detail {
		padding: 30rpx;

		.title {
			font-size: 46rpx;
			color: #333;
		}

		.info {
			background-color: #f6f6f6;
			padding: 20rpx;
			font-size: 25rpx;
			color: #666;
			display: flex;
			justify-content: space-between;
			margin: 40rpx 0;
		}

		.content {
			padding-bottom: 50rpx;
			/deep/ img{
				max-width: 100%;
			}
		}

		.description {
			background-color: #fef0f0;
			font-size: 26rpx;
			padding: 20rpx;
			color: #f89898;
			line-height: 1, 8em;
		}
	}
</style>