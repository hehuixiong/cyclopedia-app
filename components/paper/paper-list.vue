<template>
	<view class="paper-list u-f-ac" @tap="goDetail">
		<view class="paper-list-l">
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		<view class="paper-list-r">
			<view class="u-f-ac u-f-jsb">{{item.username}} <view class="time">{{item.time}}</view></view>
			<view class="u-f-ac u-f-jsb">{{item.data}}
				<template v-if="item.norednum > 0">
					<uni-badge :text="item.norednum" type="error"></uni-badge>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '../../components/uni-badge/uni-badge.vue'
	export default {
		components: {
			uniBadge
		},
		props: {
			item: Object,
			index: Number
		},
		methods: {
			goDetail () {
				uni.navigateTo({
					url: '../../pages/user-chat/user-chat'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.paper-list{
		border-bottom: 1upx solid #EEEEEE;
		padding: 20upx 0;
		.paper-list-l{
			width: 100upx;
			height: 100upx;
			margin-right: 20upx;
			flex-shrink: 0;
			flex: 0 0 100upx;
			image{
				width: 100%;
				height: 100%;
				border-radius: 100%;
			}
		}
		.paper-list-r{
			flex: 1;
			>view:nth-child(1){
				font-size: 35upx;
			}
			.time{
				color: #cbcbcb;
			}
		}
	}
</style>
