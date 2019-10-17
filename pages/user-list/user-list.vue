<template>
	<view class="body">
		<!-- tab切换 -->
		<swiper-tab
			:tabBars="tabBars"
			:tabIndex="tabIndex"
			@taptab="taptab"
			scrollItemStyle="width: 33.33%"
			scrollStyle="border-bottom: 0"
		></swiper-tab>
		<!-- 好友列表 -->
		<block v-for="(item, index) in 20" :key="index">
			<view class="user-list u-f-ac">
				<image src="../../static/demo/userpic/10.jpg" mode="widthFix" lazy-load></image>
				<view class="content">
					<view class="username">昵称</view>
					<view>
						<tag-sex-age :age="20" :sex="1"></tag-sex-age>
					</view>
				</view>
				<view class="icon iconfont icon-xuanze-yixuan u-f-ajc"></view>
			</view>
		</block>
	</view>
</template>

<script>
	import swiperTab from '../../components/index/swiper-tab.vue'
	import tagSexAge from '../../components/common/tag-sex-age.vue'
	export default {
		components: {
			swiperTab,
			tagSexAge
		},
		data() {
			return {
				tabBars: [
					{ name: '互关', id: 'huguan', num: 10 },
					{ name: '关注', id: 'guanzhu', num: 20 },
					{ name: '粉丝', id: 'fensi', num: 30 }
				],
				tabIndex: 0
			}
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
				uni.hideKeyboard() // 关闭键盘
			}
		},
		onPageScroll() {
			uni.hideKeyboard() // 关闭键盘
		},
		methods: {
			// tab点击
			taptab (index) {
				this.tabIndex = index
			}
		}
	}
</script>

<style lang="less" scoped>
	.body{
		padding: 0 20upx;
	}
	.user-list{
		padding: 20upx 0;
		border-bottom: 1upx solid #EEEEEE;
		image{
			width: 100upx;
			height: 100upx;
			border-radius: 50%;
			margin-right: 20upx;
			flex-shrink: 0;
		}
		.content{
			flex: 1;
			.username{
				font-size: 32upx;
			}
		}
		.icon-xuanze-yixuan{
			width: 80upx;
			font-size: 40upx;
		}
	}
</style>
