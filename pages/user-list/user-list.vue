<template>
	<view class="body">
		<!-- tab切换 -->
		<swiper-tab
			:tabBars="tabBars"
			:tabIndex="tabIndex"
			@taptab="taptab"
			scrollItemStyle="width: 33.33%"
			scrollStyle="border-bottom: 0"
		></swiper-tab>
		<!-- 好友列表 -->
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
								<user-list :item="item" :index="index"></user-list>
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
	import userList from '../../components/user-list/user-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	import noThing from '../../components/common/no-thing.vue'
	export default {
		components: {
			swiperTab,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				swiperHeight: 0,
				tabBars: [
					{ name: '互关', id: 'huguan', num: 10 },
					{ name: '关注', id: 'guanzhu', num: 20 },
					{ name: '粉丝', id: 'fensi', num: 30 }
				],
				tabIndex: 0,
				newsList: [
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是美女',
								age: 20,
								sex: 0,
								isattention: false
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是美女',
								age: 20,
								sex: 0,
								isattention: false
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list: [
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是美女',
								age: 20,
								sex: 0,
								isattention: false
							},
							{
								userpic: '../../static/demo/userpic/10.jpg',
								username: '我是帅哥',
								age: 22,
								sex: 1,
								isattention: true
							}
						]
					}
				]
			}
		},
		// 监听导航按钮事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
				uni.hideKeyboard() // 关闭键盘
			}
		},
		onPageScroll() {
			uni.hideKeyboard() // 关闭键盘
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
			// 上拉加载更多
			loadMore (index) {
				if (this.newsList[index].loadtext !== '上拉加载更多') return
				this.newsList[index].loadtext = '加载中...'
				let timer = setTimeout(() => {
					let obj = {
						userpic: '../../static/demo/userpic/10.jpg',
						username: '我是美女111',
						age: 20,
						sex: 0,
						isattention: false
					}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.newsList[index].loadtext = '没有更多数据了~'
			},
			// tab点击
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

<style lang="less" scoped>
</style>
