<template>
	<view
		class="icon iconfont sex-age"
		:class="[sex === 0 ? 'icon-nan' : 'icon-nv']"
	>{{age}}
	</view>
</template>

<script>
	export default {
		props: {
			sex: Number,
			age: Number
		}
	}
</script>

<style lang="less" scoped>
	.sex-age{
		background: #007AFF;
		color: #FFFFFF;
		font-size: 24upx;
		padding: 8upx 10upx;
		border-radius: 20upx;
		line-height: 20upx;
		display: inline-block;
		&.icon-nv{
			background: #ff5555;
		}
	}
</style>
