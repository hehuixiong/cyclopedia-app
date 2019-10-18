<template>
	<view>
		<template v-if="list.length > 0">
			<block v-for="(item, index) in list" :key="index">
				<index-list :item="item" :index="index"></index-list>
			</block>
			<!-- 上拉加载更多 -->
			<load-more :loadtext="loadtext"></load-more>
		</template>
		<template v-else-if="isSearch && list.length < 1">
			<!-- 无内容默认 -->
			<no-thing></no-thing>
		</template>
	</view>
</template>

<script>
	import indexList from '../../components/index/index-list.vue'
	import noThing from '../../components/common/no-thing.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		components: {
			indexList,
			noThing,
			loadMore
		},
		data() {
			return {
				isSearch: false,
				loadtext: '上拉加载更多',
				list: [],
				key_word: ''
			}
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap (e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
				uni.hideKeyboard() // 关闭键盘
			}
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged (e) {
			this.key_word = e.text
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
		onNavigationBarSearchInputConfirmed (e) {
			if (e.text) this.getData()
		},
		// 监听页面触底事件
		onReachBottom() {
			this.loadMore()
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getData()
			uni.stopPullDownRefresh()
		},
		methods: {
			getData () {
				// 请求服务器 post keyword ： this.key_word
				uni.showLoading({
					title: "加载中."
				})
				setTimeout(() => {
					let arr = [
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '昵称',
							isattention: true,
							title: '走出去，才发现你跟别人差点不是一点半点',
							type: 'video', // image 图文，video 视频
							titlepic: '../../static/demo/datapic/29.jpg',
							playnum: '20w',
							long: '2:47',
							infonum: {
								index: 1,       // 0没有操作，1顶，2：踩
								praisenum: 11,  // 顶
								tramplenum: 11  // 踩
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '昵称',
							isattention: false,
							title: '走出去，才发现你跟别人差点不是一点半点',
							type: 'video', // image 图文，video 视频
							titlepic: '../../static/demo/datapic/28.jpg',
							playnum: '20w',
							long: '2:47',
							infonum: {
								index: 2,       // 0没有操作，1顶，2：踩
								praisenum: 11,  // 顶
								tramplenum: 11  // 踩
							},
							commentnum: 10,
							sharenum: 10
						}
					]
					this.list = arr
					uni.hideLoading()
					this.isSearch = true
				}, 2000)
			},
			// 上拉加载更多
			loadMore (index) {
				if (this.loadtext !== '上拉加载更多') return
				this.loadtext = '加载中...'
				let timer = setTimeout(() => {
					let obj = {
						userpic: '../../static/demo/userpic/12.jpg',
						username: '昵称',
						isattention: false,
						title: '走出去，才发现你跟别人差点不是一点半点',
						type: 'video', // image 图文，video 视频
						titlepic: '../../static/demo/datapic/11.jpg',
						playnum: '20w',
						long: '2:47',
						infonum: {
							index: 2,       // 0没有操作，1顶，2：踩
							praisenum: 11,  // 顶
							tramplenum: 11  // 踩
						},
						commentnum: 10,
						sharenum: 10
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

<style>

</style>
