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
						<!-- 搜索框 -->
						<view class="search-input">
							<input class="uni-input" v-model="key_word" placeholder-class="icon iconfont icon-sousuo topic-search" placeholder="搜索内容" />
						</view>
						<!-- 轮播图 -->
						<swiper
							class="topic-swiper"
							indicator-color="#ff5555"
							indicator-active-color="#ffffff"
							:indicator-dots="true"
							:autoplay="true"
							:interval="3000"
							:duration="300"
							:circular="true"
						>
							<block v-for="(item, index) in topic.swiper" :key="index">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view class="title">最近更新</view>
							<block v-for="(item, index) in topic.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>
						</view>
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
	import topicNav from '../../components/news/topic-nav.vue'
	import topicList from '../../components/news/topic-list.vue'
	export default {
		components: {
			commonList,
			newsNavBar,
			loadMore,
			topicNav,
			topicList
		},
		data() {
			return {
				tabIndex: 1,
				key_word: '',
				swiperHeight: 0,
				tabBars: [
					{name: '关注', id: 'guanzhu'},
					{name: '话题', id: 'huati'},
				],
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
				topic: {
					swiper: [
						{src: '../../static/demo/banner1.jpg'},
						{src: '../../static/demo/banner2.jpg'},
						{src: '../../static/demo/banner2.jpg'},
						{src: '../../static/demo/banner1.jpg'}
					],
					nav: [
						{name: '最新'},
						{name: '游戏'},
						{name: '打卡'},
						{name: '情感'},
						{name: '故事'},
						{name: '喜爱'}
					],
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
						}
					]
				}
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
		.search-input{
			padding: 20upx;
			input{
				background: #f4f4f4;
				border-radius: 10upx;
			}
			.topic-search{
				display: flex;
				justify-content: center;
				font-size: 28upx;
			}
		}
		.topic-swiper{
			padding: 0 20upx 20upx 20upx;
			image{
				width: 100%;
			}
		}
		.topic-new{
			padding: 20upx;
			.title{
				font-size: 32upx;
				margin-bottom: 10upx;
			}
		}
	}
</style>
