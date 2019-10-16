<template>
	<view class="news">
		<uni-nav-bar :fixed="true" :border="false" :statusBar="true" @click-right="openAdd">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao"></view>
				</view>
			</block>
			<!-- 中间 -->
			<view class="nav-tab-bar u-f-ajc">
				<block v-for="(item, index) in tabBars" :key="index">
					<view class="u-f-ajc"
					@tap="changeTab(index)"
					:class="{active: tabIndex === index}"
					>{{item.name}}
						<view class="nav-tab-bar-line"></view>
					</view>
				</block>
			</view>
			<!-- 右边 -->
			<block slot="right">
				<view class="nav-right u-f-ajc">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	export default {
		components: {
			uniNavBar
		},
		data () {
			return {}
		},
		props: {
			tabBars: Array,
			tabIndex: Number
		},
		methods: {
			changeTab (index) {
				this.$emit('change-tab', index)
			},
			openAdd () {
				uni.navigateTo({
					url: '../add-input/add-input'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.news{
		.nav-left,.nav-right{
			>view{
				font-size: 40upx;
			}
		}
		.nav-left{
			margin-left: 16upx;
			>view{
				color: #FF9619;
			}
		}
		.nav-right{
			width: 100%;
		}
		.nav-tab-bar{
			position: relative;
			left: e("calc(50% - 36upx)");
			transform: translateX(-50%);
			>view{
				font-size: 30upx;
				padding: 0 12upx;
				font-weight: bold;
				color: #969696;
				&.active{
					color: #333333!important;
					.nav-tab-bar-line{
						border-bottom: 5upx solid #fede33;
						border-top: 5upx solid #fede33;
						width: 56upx;
						border-radius: 20upx;
						position: absolute;
						bottom: -4upx;
					}
				}
			}
		}
	}
</style>
