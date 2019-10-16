<template>
	<view class="load-more">{{loadtext}}</view>
</template>

<script>
	export default {
		props: {
			loadtext: String
		}
	}
</script>

<style scoped lang="less">
	.load-more{
		text-align: center;
		color: #999999;
		padding: 15upx;
	}
</style>
