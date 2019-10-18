<template>
	<view class="index-list">
		<view class="list-item1 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
				{{item.username}}
			</view>
			<view class="u-f-ac" v-show="!isattention" @tap="onattention">
				<view class="icon iconfont icon-zengjia">关注</view>
			</view>
		</view>
		<view class="list-item2" @tap="openDetail">{{item.title}}</view>
		<view class="list-item3" @tap="openDetail">
			<!-- 图片 -->
			<image :src="item.titlepic" mode="widthFix"></image>
			<!-- 视频 -->
			<template v-if="item.type === 'video'">
				<view class="play icon iconfont icon-bofang"></view>
				<view class="play-info">
					{{item.playnum}}次播放 {{item.long}}
				</view>
			</template>
		</view>
		<view class="list-item4 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<view class="u-f-ac" :class="{active: infonum.index === 1}" @tap="operation('praise', index)">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view>
					{{infonum.praisenum}}
				</view>
				<view class="u-f-ac" :class="{active: infonum.index === 2}" @tap="operation('trample', index)">
					<view class="icon iconfont icon-kulian"></view>
					{{infonum.tramplenum}}
				</view>
			</view>
			<view class="u-f-ac">
				<view class="u-f-ac">
					<view class="icon iconfont icon-pinglun1"></view>
					{{item.commentnum}}
				</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa"></view>
					{{item.sharenum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				isattention: this.item.isattention,
				infonum: this.item.infonum
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
			},
			// 顶 踩
			operation (type, index) {
				switch(type) {
					case 'praise':
					if (this.infonum.index === 1) return
					this.infonum.praisenum++
					if (this.infonum.index === 2) {
						this.infonum.tramplenum--
					}
					this.infonum.index = 1
						break
					case 'trample':
					if (this.infonum.index === 2) return
					this.infonum.tramplenum++
					if (this.infonum.index === 1) {
						this.infonum.praisenum--
					}
					this.infonum.index = 2
						break
				}
			},
			// 进入详情页
			openDetail () {
				console.log('进入详情页')
				uni.navigateTo({
					url: '../../pages/detail/detail?detailData=' + JSON.stringify(this.item)
				})
			}
		}
	}
</script>

<style scoped lang="less">
.index-list{
		padding: 20upx;
		border-bottom: 1upx solid #efefef;
		.list-item1{
			>view:first-child{
				color: #999999;
			}
			>view:first-child image{
				width: 85upx;
				height: 85upx;
				border-radius: 100%;
				margin-right: 10upx;
			}
			>view:last-child>view{
				background: #f4f4f4;
				border-radius: 5upx;
				padding: 0 10px 0 8upx;
				font-size: 28upx;
			}
		}
		.list-item2{
			padding: 10upx 0;
			font-size: 32upx;
		}
		.list-item3{
			position: relative;
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
			image{
				width: 100%;
				border-radius: 20upx;
			}
		}
		.list-item4{
			padding: 15upx 8upx;
			>view{
				color: #999999;
			}
			.active{
				color: green;
			}
			>view>view:first-child{
				margin-right: 15upx;
			}
			>view>view>view{
				margin-right: 10upx;
			}
		}
	}
</style>
