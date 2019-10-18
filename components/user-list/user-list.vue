<template>
	<view class="user-list u-f-ac">
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<view class="content">
			<view class="username">{{item.username}}</view>
			<view>
				<tag-sex-age :age="item.age" :sex="item.sex"></tag-sex-age>
			</view>
		</view>
		<view class="icon iconfont u-f-ajc"
		:class="[item.isattention ? 'icon-xuanze-yixuan' : 'icon-zengjia1']"></view>
	</view>
</template>

<script>
	import tagSexAge from '../../components/common/tag-sex-age.vue'
	export default {
		components: {
			tagSexAge
		},
		props: {
			item: Object,
			index: Number
		}
	}
</script>

<style lang="less" scoped>
	.user-list{
		margin: 0 20upx;
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
		.icon-xuanze-yixuan,.icon-zengjia1{
			width: 80upx;
			font-size: 40upx;
		}
		.icon-zengjia1{
			color: rgb(254, 228, 42)!important;
		}
	}
</style>
