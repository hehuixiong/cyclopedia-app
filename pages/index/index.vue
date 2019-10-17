<template>
	<view>
		<!-- 顶部tab start -->
		<swiper-tab
			:tabBars="tabBars"
			:tabIndex="tabIndex"
			@taptab="taptab"
		></swiper-tab>
		<!-- 顶部tab end -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box"
			:style="{height: swiperHeight + 'px'}"
			:current="tabIndex"
			@change="tabChange"
			>
				<swiper-item v-for="(items, key) in newsList" :key="key">
					<scroll-view scroll-y class="list" @scrolltolower="loadMore(key)">
						<template v-if="items.list.length > 0">
							<!-- 图文列表 -->
							<block v-for="(item, index) in items.list" :key="index">
								<index-list :item="item" :index="index"></index-list>
							</block>
							<!-- 上拉加载更多 -->
							<load-more :loadtext="items.loadtext"></load-more>
						</template>
						<template v-else>
							<!-- 无内容默认 -->
							<no-thing></no-thing>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import indexList from '../../components/index/index-list.vue'
	import swiperTab from '../../components/index/swiper-tab.vue'
	import loadMore from '../../components/common/load-more.vue'
	import noThing from '../../components/common/no-thing.vue'
	export default {
		components: {
			'index-list': indexList,
			'swiper-tab': swiperTab,
			'load-more': loadMore,
			'no-thing': noThing
		},
		data() {
			return {
				swiperHeight: 0,
				tabIndex: 0,
				tabBars: [
					{
						name: '关注',
						id: 1
					},
					{
						name: '推荐',
						id: 7
					},
					{
						name: '体育',
						id: 2
					},
					{
						name: '热点',
						id: 3
					},
					{
						name: '财经',
						id: 4
					},
					{
						name: '娱乐',
						id: 5
					},
					{
						name: '小说',
						id: 6
					}
				],
				newsList: [
					{
						loadtext: '上拉加载更多',
						list: [
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
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/27.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 2,       // 0没有操作，1顶，2：踩
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
								titlepic: '../../static/demo/datapic/26.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/25.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 2,       // 0没有操作，1顶，2：踩
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
								titlepic: '../../static/demo/datapic/24.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/23.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 2,       // 0没有操作，1顶，2：踩
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
								titlepic: '../../static/demo/datapic/21.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/20.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 2,       // 0没有操作，1顶，2：踩
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
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
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
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
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
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称',
								isattention: false,
								title: '走出去，才发现你跟别人差点不是一点半点',
								type: 'video', // image 图文，video 视频
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: '20w',
								long: '2:47',
								infonum: {
									index: 0,       // 0没有操作，1顶，2：踩
									praisenum: 11,  // 顶
									tramplenum: 11  // 踩
								},
								commentnum: 10,
								sharenum: 10
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: []
					}
				]
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight - uni.upx2px(100)
					this.swiperHeight = height
				}
			})
		},
		// 监听原生标题栏搜索输入框点击事件
		onNavigationBarSearchInputClicked () {
			uni.navigateTo({
				url: '../search/search'
			})
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap (e) {
			switch (e.index) {
				case 0:
					break
				case 1:
				uni.navigateTo({
					url: '../add-input/add-input'
				})
					break
			}
		},
		methods: {
			// 上拉加载更多
			loadMore (index) {
				if (this.newsList[index].loadtext !== '上拉加载更多') return
				this.newsList[index].loadtext = '加载中...'
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
					this.newsList[index].list.push(obj)
					this.newsList[index].loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.newsList[index].loadtext = '没有更多数据了~'
			},
			// 点击切换
			taptab (index) {
				this.tabIndex = index
			},
			// 切换改变tab
			tabChange (e) {
				this.tabIndex = e.detail.current
			}
		}
	}
</script>

<style scoped lang="less">
	
</style>
