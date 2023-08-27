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
	import {
		parseTime
	} from "@/utils/tool.js"
	console.log(parseTime(1786674746723));
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
						res.data.content = res.data.content.replace(/<img/gi, "<img style='max-width:100%'")
						res.data.posttime = parseTime(res.data.posttime, "{y}-{m}-{d} {h}:{i}:{s}")
						this.detail = res.data
						uni.setNavigationBarTitle({
							title: this.detail.title
						})

						//存储历史记录
						this.saveHistory()
					}
				})
			},
			saveHistory() {
				const historyArr = uni.getStorageSync("historyArr") || []
				const item = {
					id: this.detail.id,
					classid: this.detail.classid,
					picurl: this.detail.picurl,
					looktime: parseTime(Date.now()),
					title: this.detail.title
				}
				if (historyArr.length > 0) {
					const index = historyArr.findIndex(item1 => item1.id == item.id)
					console.log("index: ", index);
					if(index > -1) historyArr.splice(index,1)
				}
				historyArr.unshift(item)
				// historyArr = historyArr.slice(0,10)
				uni.setStorageSync("historyArr", historyArr)
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