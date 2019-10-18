<template>
	<view>
		<!-- 聊天列表 -->
		<block v-for="(item, index) in list" :key="index">
			<user-chat-list :item="item" :index="index"></user-chat-list>
		</block>
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
				list: []
			}
		},
		onLoad () {
			this.getData()
		},
		methods: {
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
				// 发送逻辑
				console.log(text)
			}
		}
	}
</script>

<style lang="less" scoped>
</style>
