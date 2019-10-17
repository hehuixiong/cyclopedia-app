<template>
	<view>
		<!-- 话题介绍 -->
		<topic-info :topicInfo="topicInfo"></topic-info>
		<!-- tabbar切换 -->
		<swiper-tab
			:tabBars="tabBars"
			:tabIndex="tabIndex"
			@taptab="taptab"
			scrollItemStyle="width: 50%"
			scrollStyle="border-bottom: 0"
		></swiper-tab>
		<!-- 列表 -->
		<view class="topic-detail-list">
			<block v-for="(items, key) in tabList" :key="key">
				<template v-if="tabIndex === key">
					<!-- 列表 -->
					<block v-for="(item, index) in items.list" :key="index">
						<common-list :item="item" :index="index"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="items.loadtext"></load-more>
				</template>
			</block>
		</view>
	</view>
</template>

<script>
	import topicInfo from '../../components/topic/topic-info.vue'
	import swiperTab from '../../components/index/swiper-tab.vue'
	import commonList from '../../components/common/common-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		components: {
			topicInfo,
			swiperTab,
			commonList,
			loadMore
		},
		data() {
			return {
				topicInfo: {
					titlepic: '../../static/demo/userpic/10.jpg',
					title: '亿往事，敬余生',
					desc: '面试官：在电梯里巧遇马云你会做什么？90后女孩的回答当初被录用',
					totalnum: 2000,
					todaynum: 8989
				},
				tabIndex: 0,
				tabBars: [
					{ name: '默认', id: 'moren' },
					{ name: '最新', id: 'zuixin' }
				],
				tabList: [
					{
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
							}
						]
					},
					{
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
							}
						]
					}
				]
			}
		},
		// 上拉触底事件
		onReachBottom() {
			// 上拉加载
			this.loadMore()
		},
		// 下拉刷新
		onPullDownRefresh() {
			this.getData()
		},
		methods: {
			// 上拉刷新
			getData () {
				// 获取数据
				let arr = [
					{
						userpic: '../../static/demo/userpic/12.jpg',
						usrename: '我是昵称111',
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
						usrename: '我是昵称222',
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
					}
				]
				// 关闭下拉刷新
				setTimeout(() => {
					// 赋值
					this.tabList[this.tabIndex].list = [...arr]
					uni.stopPullDownRefresh() // 停在转圈圈
				}, 2000)
			},
			// 上拉加载
			loadMore () {
				if (this.tabList[this.tabIndex].loadtext !== '上拉加载更多') return
				this.tabList[this.tabIndex].loadtext = '加载中...'
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
					this.tabList[this.tabIndex].list.push(obj)
					this.tabList[this.tabIndex].loadtext = '上拉加载更多'
					clearTimeout(timer)
				}, 1000)
				// this.tabList[this.tabIndex].loadtext = '没有更多数据了~'
			},
			// 点击切换
			taptab (index) {
				this.tabIndex = index
			}
		}
	}
</script>

<style lang="less" scoped>

</style>
