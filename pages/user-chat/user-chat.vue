<template>
	<view>
		<!-- 聊天列表 -->
		<scroll-view
		id="scrollview"
		scroll-y
		:scroll-top="scrollTop"
		:scroll-with-animation="true"
		:style="{height: style.contentH + 'px'}"
		>
			<block v-for="(item, index) in list" :key="index">
				<user-chat-list :item="item" :index="index"></user-chat-list>
			</block>
		</scroll-view>
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import userChatList from '../../components/user-chat/user-chat-list.vue'
	import time from '../../common/time.js'
	export default {
		components: {
			userChatBottom,
			userChatList
		},
		data() {
			return {
				scrollTop: 0,
				list: [],
				style: {
					contentH: 0,
					itemH: 0
				}
			}
		},
		onLoad () {
			this.getData()
			this.initData()
		},
		onReady() {
			this.pageToBottom()
		},
		methods: {
			// 初始化参数
			initData () {
				try {
					const res = uni.getSystemInfoSync()
					this.style.contentH = res.windowHeight - uni.upx2px(88)
				} catch (e) {}
			},
			pageToBottom () {
				this.style.itemH = 0
				let q = uni.createSelectorQuery()
				q.select('#scrollview').boundingClientRect()
				q.selectAll('.user-chat-item').boundingClientRect()
				q.exec((res) => {
					res[1].map((e) => {
						this.style.itemH += e.height
					})
					if (this.style.itemH > this.style.contentH) {
						this.scrollTop = this.style.itemH
					}
				})
			},
			getData () {
				// 服务器拿到的数据
				let arr = [
					{
						isme: false,
						userpic: '../../static/demo/userpic/11.jpg',
						type: 'text',
						data: '你好，我喜欢你',
						time: '1554970012' //php 生成的时间戳10位数
					},
					{
						isme: true,
						userpic: '../../static/demo/userpic/10.jpg',
						type: 'img',
						data: '../../static/demo/1.jpg',
						time: '1571365818' //php 生成的时间戳10位数
					},
					{
						isme: true,
						userpic: '../../static/demo/userpic/10.jpg',
						type: 'text',
						data: '我不喜欢你',
						time: '1571365819' //php 生成的时间戳10位数
					}
				]
				for (var i = 0; i < arr.length; i++) {
					this.$set(arr[i], 'gstime', time.gettime.getChatTime(arr[i].time, i > 0 ? arr[i - 1].time : 0))
				}
				this.list = arr
			},
			submit (text) {
				if (text) {
					// 发送逻辑
					console.log(text)
					// 构建数据
					let now = new Date().getTime()
					let obj = {
						isme: true,
						userpic: '../../static/demo/userpic/10.jpg',
						type: 'text',
						data: text,
						time: now, //php 生成的时间戳10位数
						gstime: time.gettime.getChatTime(now, this.list[this.list.length - 1].time)
					}
					this.list.push(obj)
					this.pageToBottom()
				}
			}
		}
	}
</script>

<style lang="less" scoped>
</style>
