<template>
	<view class="topic-nav">
		<view class="u-f-ac u-f-jsb">
			<view>热门分类</view>
			<view class="u-f-ac" @tap="openTopicNav">更多<view class="icon iconfont icon-jinru"></view></view>
		</view>
		<view class="u-f-ac">
			<block v-for="(item, index) in nav" :key="index">
				<view>{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			nav: Array
		},
		methods: {
			openTopicNav () {
				uni.navigateTo({
					url: '../../pages/topic-nav/topic-nav'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.topic-nav{
		border-top: 1upx solid #EEEEEE;
		border-bottom: 1upx solid #EEEEEE;
		padding: 20upx;
		>view:first-child{
			margin-bottom: 15upx;
			>view:first-child{
				color: #333333;
				font-size: 32upx;
			}
			>view:last-child{
				color: #999999;
			}
		}
		>view:last-child{
			>view{
				flex: 1;
				text-align: center;
				background: #EEEEEE;
				color: #9e9e9e;
				border-radius: 10upx;
				margin: 0 10upx;
			}
		}
	}
</style>
