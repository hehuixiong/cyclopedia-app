<template>
	<view class="topic-list u-f" @tap="goDetail">
		<view class="topic-list-l">
			<image :src="item.titlepic" mode="widthFix" lazy-load></image>
		</view>
		<view class="topic-list-r">
			<view class="title">{{item.title}}{{index}}</view>
			<view class="desc">{{item.desc}}</view>
			<view class="dynamic">动态 {{item.totalnum}} 今日 {{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods: {
			goDetail () {
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.topic-list{
		border-bottom: 1upx solid #EEEEEE;
		padding: 16upx 0;
		.topic-list-l {
			width: 160upx;
			height: 160upx;
			margin-right: 20upx;
			flex: 0 0 160upx;
			image{
				width: 100%;
				height: 100%;
				border-radius: 10upx;
			}
		}
		.topic-list-r {
			flex: 1;
			padding-top: 8upx;
			color: #A4A4A4;
			view{
				line-height: 46upx;
			}
			.title {
				color: #333333;
				font-size: 32upx;
			}
		}
	}
</style>
