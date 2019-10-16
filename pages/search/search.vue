<template>
	<view>
		<view @tap="test">搜索1</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap (e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
			}
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged (e) {
			console.log(e.text)
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
		onNavigationBarSearchInputConfirmed (e) {
			console.log(e.text)
		},
		methods: {
			test () {
				uni.navigateBack({
					delta: 1
				})
			}
		}
	}
</script>

<style>

</style>
