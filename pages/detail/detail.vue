<template>
	<view class="detail">
		<view class="title">
			FJIOWDEHGFIOREDSJGVLSDJGPERW'UJSGP'
		</view>
		<view class="info">
			<view class="author">编辑: 张三</view>
			<view class="time">2023年8月27日00:13:06</view>
		</view>
		<view class="content">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolorem adipisci similique, voluptas mollitia natus at et nulla odit in a! Quibusdam assumenda aspernatur architecto obcaecati quas repudiandae dolor alias vel?
		</view>
		<view class="description">声明:本站的内容均采集于腾讯新闻,如果侵权请联系管理(leizhuzheng@qq.com)进行整改删除,本站进行的内容采集不代表本站及作者观点,若有侵犯请及时联系管理员,谢谢您的支持</view>
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
.detail{
	padding: 30rpx;
	.title{
		font-size: 46rpx;
		color: #333;
	}
	.info{
		background-color: #f6f6f6;
		padding: 20rpx;
		font-size: 25rpx;
		color: #666;
		display: flex;
		justify-content: space-between;
		margin: 40rpx 0;
	}
	.content{
		padding-bottom: 50rpx;
	}
	.description{
		background-color: #fef0f0;
		font-size: 26rpx;
		padding: 20rpx;
		color: #f89898;
		line-height: 1,8em;
	}
}
</style>