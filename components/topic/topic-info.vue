<template>
	<view>
		<!-- 模糊背景 -->
		<view class="topic-bg">
			<image :src="topicInfo.titlepic" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<view class="topic-info">
			<view class="topic-info-t u-f-ac">
				<image :src="topicInfo.titlepic" mode="widthFix" lazy-load></image>
				<view class="title">#{{topicInfo.title}}#</view>
			</view>
			<view class="topic-info-c u-f-ac">
				<view>动态 {{topicInfo.totalnum}}</view>
				<view>今日 {{topicInfo.todaynum}}</view>
			</view>
			<view class="topic-info-b">
				<view>{{topicInfo.desc}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			topicInfo: Object
		}
	}
</script>

<style lang="less" scoped>
	.topic-bg{
		width: 100%;
		height: 300upx;
		position: relative;
		overflow: hidden;
		image{
			width: 100%;
			position: absolute;
			filter: blur(10px); // 模糊
		}
	}
	.topic-info{
		padding: 0 20upx;
		.topic-info-t{
			position: relative;
			image{
				width: 160upx;
				height: 160upx;
				border-radius: 20upx;
				position: absolute;
				top: -80upx;
			}
			.title{
				font-size: 30upx;
				margin-left: 180upx;
				flex: 1;
			}
		}
		.topic-info-c{
			padding: 32upx 0 14upx 0;
			>view{
				color: #cdcdcd;
			}
		}
		.topic-info-b{
			font-size: 32upx;
			color: #a3a3a3;
			padding-bottom: 10upx;
		}
	}
</style>
