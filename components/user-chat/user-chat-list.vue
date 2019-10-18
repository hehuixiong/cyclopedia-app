<template>
	<view class="user-chat-item">
		<view v-if="item.gstime" class="user-chat-time">{{item.gstime}}</view>
		<view class="user-chat-list u-f" :class="{'user-chat-me': item.isme}">
			<view class="userpic" v-if="!item.isme">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
			</view>
			<view class="user-chat-list-body">
				<!-- 文字 -->
				<text v-if="item.type === 'text'">{{item.data}}</text>
				<!-- 图片 -->
				<image v-if="item.type === 'img'" :src="item.data" mode="widthFix"></image>
			</view>
			<view class="userpic" v-if="item.isme">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		}
	}
</script>

<style lang="less" scoped>
	.user-chat-time{
		padding-top: 20upx;
		color: #a2a2a2;
		font-size: 24upx;
		text-align: center;
	}
	.user-chat-list{
		padding: 20upx;
		.userpic{
			width: 80upx;
			height: 80upx;
			flex-shrink: 0;
			image{
				width: 100%;
				height: 100%;
				border-radius: 50%;
			}
		}
		.user-chat-list-body{
			position: relative;
			background: #f4f4f4;
			padding: 16upx 24upx;
			margin-left: 20upx;
			border-radius: 20upx;
			margin-right: 150upx;
			image{
				max-width: 200upx;
				max-height: 300upx;
			}
			&:after{
				position: absolute;
				left: -30upx;
				top: 30upx;
				right: 0;
				content: '';
				width: 0;
				height: 0;
				border: 16upx solid #f4f4f4;
				border-color:  transparent #f4f4f4 transparent transparent;
			}
		}
	}
	.user-chat-me{
		justify-content: flex-end;
		.user-chat-list-body{
			margin-right: 20upx;
			margin-left: 150upx;
			&:after{
				left: auto;
				right: -30upx;
				border-color:  transparent transparent transparent #f4f4f4;
			}
		}
	}
</style>
