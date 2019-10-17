<template>
	<view class="common-list u-f">
		<view class="common-list-l">
			<image
				:src="item.userpic"
				mode="widthFix"
				lazy-load>
			</image>
		</view>
		<view class="common-list-r">
			<view class="u-f-ac u-f-jsb list-r-item1">
				<view class="u-f-ac nickname">
					<view style="margin-right: 10upx;">{{item.usrename}}</view>
					<tag-sex-age :age="item.age" :sex="item.sex"></tag-sex-age>
				</view>
				<view
					class="icon iconfont icon-zengjia attention"
					v-show="!isattention"
					@tap="onattention"
				>关注</view>
			</view>
			<view class="title list-r-item2">{{item.title}}</view>
			<view class="list-r-item3">
				<!-- 图片 -->
				<template>
					<image
						v-if="item.titlepic"
						:src="item.titlepic"
						mode="widthFix"
						lazy-load>
					</image>
				</template>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="play icon iconfont icon-bofang"></view>
					<view class="play-info">
						{{item.video.looknum}}次播放 {{item.video.long}}
					</view>
				</template>
				<!-- 分享 -->
				<view class="common-list-share u-f-ac" v-if="item.share">
					<image
						:src="item.share.titlepic"
						mode="widthFix"
						lazy-load>
						</image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<view class="u-f-ac u-f-jsb list-r-item4">
				<view class="site">{{item.path}}</view>
				<view class="u-f-ac right">
					<view class="u-f-ac">
						<view class="icon iconfont icon-zhuanfa"></view>
						{{item.sharenum}}
					</view>
					<view class="u-f-ac">
						<view class="icon iconfont icon-pinglun1"></view>
						{{item.commentnum}}
					</view>
					<view class="u-f-ac">
						<view class="icon iconfont icon-dianzan"></view>
						{{item.goodnum}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tagSexAge from './tag-sex-age.vue'
	export default {
		components: {
			tagSexAge
		},
		data () {
			return {
				isattention: this.item.isattention
			}
		},
		props: {
			item: Object,
			index: Number
		},
		methods: {
			// 关注
			onattention () {
				this.isattention = true
				uni.showToast({
					title: '关注成功'
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.common-list{
		padding: 20upx;
		.common-list-l{
			flex-shrink: 0; // 防止被压缩
			image{
				width: 90upx;
				height: 90upx;
				border-radius: 100%;
			}
		}
		.common-list-r{
			flex: 1;
			margin-left: 15upx;
			border-bottom: 1upx solid #EEEEEE;
			padding-bottom: 10upx;
			.list-r-item1 {
				.nickname{
					color: #999999;
					font-size: 30upx;
				}
				.attention{
					background: #f4f4f4;
					border-radius: 5upx;
					padding: 0 10px 0 8upx;
					font-size: 28upx;
				}
			}
			.list-r-item2.title {
				margin: 12upx 0;
				font-size: 30upx;
			}
			.list-r-item3 {
				position: relative;
				margin-bottom: 10upx;
				image{
					width: 100%;
					border-radius: 10upx;
				}
				.play{
					position: absolute;
					font-size: 100upx;
					color: #FFFFFF;
					left: 50%;
					top: 50%;
					transform: translate(-50%, -50%);
				}
				.play-info{
					position: absolute;
					background: rgba(51,51,51, 0.72);
					color: #FFFFFF;
					bottom: 30upx;
					right: 18upx;
					border-radius: 40upx;
					font-size: 24upx;
					padding: 0 12upx;
				}
				.common-list-share{
					background: #EEEEEE;
					padding: 10upx;
					border-radius: 10upx;
					image{
						width: 200upx;
						height: 150upx;
						margin-right: 10upx;
					}
				}
			}
			.list-r-item4 {
				font-size: 24upx;
				color: #AAAAAA;
				padding-right: 8upx;
				.site{}
				.right>view{
					margin-left: 12upx;
					padding-left: 8upx;
					font-size: 28upx;
					>view{
						padding-right: 6upx;
					}
				}
			}
		}
	}
</style>
