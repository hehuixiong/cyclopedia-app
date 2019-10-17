<template>
	<view>
		好友列表
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
			}
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
