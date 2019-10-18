<template>
	<view>
		内容页面
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad(e) {
			this.initData(JSON.parse(e.detailData))
		},
		// 监听导航右侧按钮
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				console.log('点击了')
			}
		},
		methods: {
			// 初始化数据
			initData (obj) {
				uni.setNavigationBarTitle({ title: obj.title })
			}
		}
	}
</script>

<style>

</style>
