<template>
	<view id="news">
		<!-- 自定义导航栏 -->
		<news-nav-bar
			:tabBars="tabBars"
			:tabIndex="tabIndex"
			@change-tab="changeTab"
		></news-nav-bar>
		<!-- 列表 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box"
				:style="{height: swiperHeight + 'px'}"
				:current="tabIndex"
				@change="tabChange"
			>
				<!-- 关注 -->
				<swiper-item>
					<scroll-view scroll-y class="list" @scrolltolower="loadMore">
						<block v-for="(item, index) in attention.list" :key="index">
							<common-list :item="item" :index="index"></common-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadtext="attention.loadtext"></load-more>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<scroll-view scroll-y class="list">
						<block v-for="(item, index) in attention.list" :key="index">
							<common-list :item="item" :index="index"></common-list>
						</block>
						<!-- 上拉加载 -->
						<load-more :loadtext="attention.loadtext"></load-more>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import commonList from '../../components/common/common-list.vue'
	import newsNavBar from '../../components/news/news-nav-bar.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		components: {
			commonList,
			newsNavBar,
			loadMore
		},
		data() {
			return {
				tabIndex: 0,
				swiperHeight: 0,
				attention: {
					loadtext: '上拉加载更多',
					list: [
						{
							userpic: '../../static/demo/userpic/12.jpg',
							usrename: '我是昵称',
							sex: 0, // 1男，0女
							age: 25,
							isattention: false,
							title: '我是标题',
							titlepic: '../../static/demo/datapic/1.jpg',
							video: {
								looknum: '20w',
								long: '20:44'
							},
							share: false,
							path: '广州 白云',
							sharenum: 20,
							commentnum: 30,
							goodnum: 33
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							usrename: '我是昵称',
							sex: 1, // 1男，0女
							age: 25,
							isattention: false,
							title: '我是标题',
							titlepic: '',
							video: false,
							share: {
								title: '我是分享的标题',
								titlepic: '../../static/demo/datapic/14.jpg' 
							},
							path: '广州 白云',
							sharenum: 20,
							commentnum: 30,
							goodnum: 33
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							usrename: '我是昵称',
							sex: 0, // 1男，0女
							age: 25,
							isattention: false,
							title: '我是标题',
							titlepic: '',
							video: false,
							share: {
								title: '我是分享的标题',
								titlepic: '../../static/demo/datapic/14.jpg' 
							},
							path: '广州 白云',
							sharenum: 20,
							commentnum: 30,
							goodnum: 33
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							usrename: '我是昵称',
							sex: 1, // 1男，0女
							age: 25,
							isattention: false,
							title: '我是标题',
							titlepic: '../../static/demo/datapic/1.jpg',
							video: {
								looknum: '20w',
								long: '20:44'
							},
							share: false,
							path: '广州 白云',
							sharenum: 20,
							commentnum: 30,
							goodnum: 33
						}
					]
				},
				tabBars: [
					{name: '关注', id: 'guanzhu'},
					{name: '话题', id: 'huati'},
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
			// 点击tab
			tabChange (e) {
				this.tabIndex = e.detail.current
			},
			// 滑动切换
			changeTab (index) {
				this.tabIndex = index
			},
			// 上拉加载更多
			loadMore () {
				if (this.attention.loadtext !== '上拉加载更多') return
				this.attention.loadtext = '加载中...'
				let timer = setTimeout(() => {
					let obj = {
						userpic: '../../static/demo/userpic/12.jpg',
						usrename: '我是昵称',
						sex: 1, // 1男，0女
						age: 25,
						isattention: false,
						title: '我是标题',
						titlepic: '../../static/demo/datapic/1.jpg',
						video: {
							looknum: '20w',
							long: '20:44'
						},
						share: false,
						path: '广州 白云',
						sharenum: 20,
						commentnum: 30,
						goodnum: 33
					}
					this.attention.list.push(obj)
					this.attention.loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.attention.loadtext = '没有更多数据了~'
			}
		}
	}
</script>

<style lang="less">
	#news{
	}
</style>
