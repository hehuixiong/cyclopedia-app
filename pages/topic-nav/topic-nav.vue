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
							<!-- 话题列表 -->
							<block v-for="(item, index) in items.list" :key="index">
								<topic-list class="topic-list" :item="item" :index="index"></topic-list>
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
	import swiperTab from '../../components/index/swiper-tab.vue'
	import noThing from '../../components/common/no-thing.vue'
	import loadMore from '../../components/common/load-more.vue'
	import topicList from '../../components/news/topic-list.vue'
	export default {
		components: {
			swiperTab,
			loadMore,
			noThing,
			topicList
		},
		data() {
			return {
				tabIndex: 0,
				tabBars: [
					{name: '关注', id: 1},
					{name: '推荐', id: 2},
					{name: '体育', id: 3},
					{name: '热点', id: 4},
					{name: '财经', id: 5},
					{name: '娱乐', id: 6},
					{name: '小说', id: 7}
				],
				newsList: [
					{
						loadtext: '上拉加载更多',
						list: [
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							},
							{
								titlepic: '../../static/demo/userpic/10.jpg',
								title: '话题名称',
								desc: '我是话题描述',
								totalnum: 20,
								todaynum: 20
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: []
					},
					{
						loadtext: '上拉加载更多',
						list: []
					},
					{
						loadtext: '上拉加载更多',
						list: []
					},
					{
						loadtext: '上拉加载更多',
						list: []
					},
					{
						loadtext: '上拉加载更多',
						list: []
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
		methods: {
			// 点击切换
			taptab (index) {
				this.tabIndex = index
			},
			// 切换改变tab
			tabChange (e) {
				this.tabIndex = e.detail.current
			},
			// 上拉加载更多
			loadMore (index) {
				if (this.newsList[index].loadtext !== '上拉加载更多') return
				this.newsList[index].loadtext = '加载中...'
				let timer = setTimeout(() => {
					let obj = {
						titlepic: '../../static/demo/userpic/4.jpg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 20,
						todaynum: 20
					}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.newsList[index].loadtext = '没有更多数据了~'
			}
		}
	}
</script>

<style scoped lang="less">
	.topic-list{
		padding: 20upx;
	}
</style>
