<template>
	<view id="addInput">
		<!-- 自定导航栏 -->
		<uni-nav-bar :border="false" :fixed="true" :statusBar="true" rightText="发布" @click-left="back" @click-right="submit">
			<view slot="left" class="cancel">取消</view>
			<view class="visible u-f-ajc" @tap="changeLook">
				{{visible}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!-- 多行输入框 -->
		<view class="uni-textarea">
			<textarea :focus='setFocus' v-model="textarea" placeholder="说一句话吧~" />
		</view>
		<!-- 上传多图 -->
		<uploud-images @uploud="uploud"></uploud-images>
		<!-- 弹窗 -->
		<uni-popup :show="showPopup" position="middle" mode="fixed" @hidePopup="hidePopup()">
			<view class="announcement">
				<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view>1、涉及黄色，政治，广告及骚扰信息</view>
				<view>2、涉及黄色，政治，广告及骚扰信息</view>
				<view>3、涉及黄色，政治，广告及骚扰信息</view>
				<view>4、涉及黄色，政治，广告及骚扰信息</view>
				<button type="default" @tap="hidePopup">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	import uploudImages from "../../components/common/uploud-images.vue"
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	const itemList = ['所有人可见', '仅自己可见']
	export default {
		components: {
			uniNavBar,
			uploudImages,
			uniPopup
		},
		data() {
			return {
				setFocus: false,
				isGet: false,
				visible: '所有人可见',
				textarea: '',
				imgList: [],
				showPopup: true
			}
		},
		onBackPress () {
			// 判断是否有值
			if (!this.textarea && this.imgList.length < 1) return
			if (!this.isGet) {
				this.save()
				return true
			}
		},
		onPageScroll() {
			uni.hideKeyboard() // 关闭键盘
		},
		methods: {
			// 保存为草稿
			save () {
				uni.showModal({
					content: '是否要保存为草稿',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {
						if (res.confirm) {
							console.log('保存')
						} else {
							console.log('不保存')
						}
						this.isGet = true
						this.back()
					}
				})
			},
			// 返回
			back () {
				uni.navigateBack({
					delta: 1
				})
				uni.hideKeyboard() // 关闭键盘
			},
			// 发布
			submit () {
				console.log('发布')
			},
			// 隐私
			changeLook () {
				uni.showActionSheet({
				    itemList: itemList,
				    success: (res) => {
							this.visible = itemList[res.tapIndex]
				    }
				})
			},
			uploud (list) {
				this.imgList = list
				console.log(list)
			},
			hidePopup () {
				this.showPopup = false
				this.setFocus = true
			}
		}
	}
</script>

<style lang="less" scoped>
	.cancel{
		padding-left: 20upx;
	}
	.submit{
		color: #FFFFFF;
		background: #09bb07;
		padding: 2upx 8upx;
		border-radius: 8upx;
		font-weight: bold;
	}
	.visible{
		position: absolute;
		left: 50%;
		transform: translateX(-50%);
	}
	.announcement{
		width: 520upx;
		image{
			width: 70%;
			margin-bottom: 20upx;
		}
		button{
			background: #ffe934;
			border: none;
			color: #171606;
			margin-top: 20upx;
			line-height: 80upx;
			font-size: 32upx;
		}
	}
</style>
