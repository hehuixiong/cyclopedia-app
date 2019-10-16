<template>
	<view class="uni-tab-bar">
		<scroll-view scroll-x class="uni-swiper-tab" scroll-with-animation>
			<block v-for="(tab, index) in tabBars" :key="index">
				<view class="swiper-tab-list"
				:class="{active: tabIndex === index}"
				@tap="tabtap(index)"
			>
				{{tab.name}}
				<view class="swiper-tab-line"></view>
			</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props: {
			tabBars: Array,
			tabIndex: Number
		},
		methods: {
			tabtap (index) {
				this.$emit('tabtap', index)
			}
		}
	}
</script>

<style scoped lang="less">
	.uni-swiper-tab{
		border-bottom: 1px solid #EEEEEE;
	}
	.swiper-tab-list{
		color: #969696;
		font-weight: bold;
		&.active{
			color: #343434;
			.swiper-tab-line{
				border-bottom: 6upx solid #fede33;
				width: 70upx;
				margin: 0 auto;
				border-radius: 20upx;
			}
		}
	}
</style>
