<template>
	<view>
		<view class="paper-left-popup-mask" v-show="show" @tap="hidePopup"></view>
		<view class="paper-left-popup" v-show="show">
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="addFriend">
				<view class="icon iconfont icon-sousuo"></view> 加糗友
			</view>
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="clear">
				<view class="icon iconfont icon-qingchu"></view> 清除全部
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			show: Boolean
		},
		methods: {
			hidePopup () {
				this.$emit('hide')
			},
			addFriend () {
				this.$emit('addFriend')
			},
			clear () {
				this.$emit('clear')
			}
		}
	}
</script>

<style lang="less" scoped>
	.paper-left-popup-mask{
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		z-index: 1999;
	}
	.paper-left-popup{
		position: fixed;
		right: 0;
		top: 10upx;
		background: #FFFFFF;
		z-index: 2000;
		width: 55%;
		box-shadow: 1upx 1upx 20upx 2upx #CCCCCC;
		>view{
			padding: 20upx;
			font-size: 32upx;
			>view{
				margin-right: 10upx;
				font-weight: bold;
			}
		}
		.paper-left-popup-h{
			background: #EEEEEE;
		}
	}
</style>
