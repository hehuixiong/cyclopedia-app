<template>
	<view class="body">
		<!-- 操作菜单 -->
		<paper-left-popup
			:show="show"	
			@hide="hidePopup"
			@addFriend="addFriend"
			@clear="clear"
		>
		</paper-left-popup>
		<!-- 小纸条列表 -->
		<block v-for="(item, index) in list" :index="index" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
	import paperList from '../../components/paper/paper-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	import paperLeftPopup from '../../components/paper/paper-left-popup.vue'
	export default {
		components: {
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				show: false,
				loadtext: '上拉加载更多',
				list: [
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '0'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '0'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '66'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					}
				]
			}
		},
		onReachBottom() {
			this.loadMore()
		},
		// 下拉刷新
		onPullDownRefresh() {
			this.getData()
		},
		// 监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 0:
				this.hidePopup()
				uni.navigateTo({
					url: '../user-list/user-list'
				})
					break
				case 1:
				this.show = !this.show
					break
			}
		},
		methods: {
			// 操作菜单
			addFriend () {
				console.log('加糗友')
				this.hidePopup()
			},
			clear () {
				console.log('清除全部')
				this.hidePopup()
			},
			hidePopup () {
				this.show = false
			},
			showPopup () {
				this.show = true
			},
			getData () {
				let arr = [
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称111',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称222',
						time: '10:20',
						data: '我是信息',
						norednum: '0'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称333',
						time: '10:20',
						data: '我是信息',
						norednum: '0'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '66'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					},
					{
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					}
				]
				// 关闭下拉刷新
				setTimeout(() => {
					// 赋值
					this.list = [...arr]
					uni.stopPullDownRefresh() // 停在转圈圈
				}, 2000)
			},
			// 上拉加载更多
			loadMore () {
				if (this.loadtext !== '上拉加载更多') return
				this.loadtext = '加载中...'
				let timer = setTimeout(() => {
					let obj = {
						userpic: '../../static/demo/userpic/10.jpg',
						username: '昵称',
						time: '10:20',
						data: '我是信息',
						norednum: '9999'
					}
					this.list.push(obj)
					this.loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.loadtext = '没有更多数据了~'
			}
		}
	}
</script>

<style lang="less" scoped>
	.body{
		padding: 0 20upx;
	}
</style>
