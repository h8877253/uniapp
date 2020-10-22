<template>
	<view>
		<view class="cu-bar search " style="position: fixed;top: 0;z-index: 999;width: 100%;">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input @focus="InputFocus" @blur="InputBlur" :adjust-position="false" type="text" placeholder="名称 / 代码 / 基金经理 / 功能 / 咨询"
				 confirm-type="search"></input>
			</view>
		</view>
		<view class="bg-img bg-mask flex align-center" style="background-image: url('static/topBG.jpg');height: 360upx;">
			<view class="flex align-center text-white" style="padding-top: 100upx">
				<view class="padding-lg">
					<view class="text-xl">
						服务 1亿+
					</view>
					<view class="text-lg">
						累计分红 1000亿+
					</view>
				</view>
				<view class="radius" style="margin-left: 120upx;">
					<button class="cu-btn lines-white round shadow" style="width: 240upx;">&nbsp&nbsp登录&nbsp&nbsp / &nbsp&nbsp注册&nbsp&nbsp</button>
				</view>
			</view>
		</view>
		<view class="cu-list grid no-border" :class="['col-' + gridCol]">
			<view class="cu-item" v-for="(item,index) in cuIconList" :key="index" v-if="index<gridCol*2">
				<view :class="['cuIcon-' + item.cuIcon,'text-' + item.color]">
					<view class="cu-tag badge" v-if="item.badge!=0">
						<block v-if="item.badge!=1">{{item.badge>99?'99+':item.badge}}</block>
					</view>
				</view>
				<text>{{item.name}}</text>
			</view>
		</view>
		<swiper class="card-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="false" :circular="true"
		 :autoplay="true" interval="5000" duration="500" @change="cardSwiper" indicator-color="#8799a3"
		 indicator-active-color="#0081ff">
			<swiper-item v-for="(item,index) in swiperList" :key="index" :class="cardCur==index?'cur':''">
				<view class="swiper-item">
					<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
					<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
				</view>
			</swiper-item>
		</swiper>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				cardCur: 0,
				swiperList: [{
						id: 0,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2020/09/ZwNm-kcR8ChhEfvy7A5sw..g.jpg'
					}, {
						id: 1,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2020/08/8f-xwMrRluywZ4hjO8h5A..W.jpg',
					}, {
						id: 2,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2020/08/2EfE-X3R6WbMpnXquFIXg..G.jpg'
					}, {
						id: 3,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2020/05/bRBBc9dS2mlvzRg_HdVCA..U.jpg	'
					}, {
						id: 4,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2020/05/TJJ3XHyT1ScPoc75eDeXA..B.jpg'
					}, {
						id: 5,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2019/05/IyNUXnZTC26X5LpPCTc8A..2.jpg'
					},
					{
						id: 6,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2019/05/UFwHa7BSKiLzXlCJkMqig..C.jpg'
					},
					{
						id: 7,
						type: 'image',
						url: 'http://www.lionfund.com.cn/pc/upload/2019/03/XqsT8g-QsqMYk9q72xzKA..j.jpg'
					},
				],
				cuIconList: [
					{
					cuIcon: 'friendaddfill',
					color: 'red',
					badge: 0,
					name: '开户'
				}, 
				{
					cuIcon: 'redpacket_fill',
					color: 'red',
					badge: 0,
					name: '现金宝'
				}, 
				{
					cuIcon: 'goodsfill',
					color: 'red',
					badge: 0,
					name: '稳健理财'
				}, {
					cuIcon: 'pay',
					color: 'red',
					badge: 0,
					name: '固收+'
				}, {
					cuIcon: 'writefill',
					color: 'red',
					badge: 0,
					name: '股基严选'
				}, {
					cuIcon: 'sponsorfill',
					color: 'red',
					badge: 0,
					name: '买基金'
				}, {
					cuIcon: 'settingsfill',
					color: 'red',
					badge: 0,
					name: '司南投顾'
				}, {
					cuIcon: 'moneybagfill',
					color: 'red',
					badge: 0,
					name: '尊享理财'
				}, {
					cuIcon: 'presentfill',
					color: 'red',
					badge: 0,
					name: '热门活动'
				}, {
					cuIcon: 'more',
					color: 'red',
					badge: 0,
					name: '更多'
				}],
				dotStyle: false,
				towerStart: 0,
				direction: '',
				gridCol: 5
			};
		},
		onLoad() {
			this.TowerSwiper('swiperList');
			// 初始化towerSwiper 传已有的数组名即可
		},
		methods: {
			DotStyle(e) {
				this.dotStyle = e.detail.value
			},
			// cardSwiper
			cardSwiper(e) {
				this.cardCur = e.detail.current
			},
			// towerSwiper
			// 初始化towerSwiper
			TowerSwiper(name) {
				let list = this[name];
				for (let i = 0; i < list.length; i++) {
					list[i].zIndex = parseInt(list.length / 2) + 1 - Math.abs(i - parseInt(list.length / 2))
					list[i].mLeft = i - parseInt(list.length / 2)
				}
				this.swiperList = list
			},

			// towerSwiper触摸开始
			TowerStart(e) {
				this.towerStart = e.touches[0].pageX
			},

			// towerSwiper计算方向
			TowerMove(e) {
				this.direction = e.touches[0].pageX - this.towerStart > 0 ? 'right' : 'left'
			},

			// towerSwiper计算滚动
			TowerEnd(e) {
				let direction = this.direction;
				let list = this.swiperList;
				if (direction == 'right') {
					let mLeft = list[0].mLeft;
					let zIndex = list[0].zIndex;
					for (let i = 1; i < this.swiperList.length; i++) {
						this.swiperList[i - 1].mLeft = this.swiperList[i].mLeft
						this.swiperList[i - 1].zIndex = this.swiperList[i].zIndex
					}
					this.swiperList[list.length - 1].mLeft = mLeft;
					this.swiperList[list.length - 1].zIndex = zIndex;
				} else {
					let mLeft = list[list.length - 1].mLeft;
					let zIndex = list[list.length - 1].zIndex;
					for (let i = this.swiperList.length - 1; i > 0; i--) {
						this.swiperList[i].mLeft = this.swiperList[i - 1].mLeft
						this.swiperList[i].zIndex = this.swiperList[i - 1].zIndex
					}
					this.swiperList[0].mLeft = mLeft;
					this.swiperList[0].zIndex = zIndex;
				}
				this.direction = ""
				this.swiperList = this.swiperList
			},
		}
	}
</script>

<style>
	.tower-swiper .tower-item {
		transform: scale(calc(0.5 + var(--index) / 10));
		margin-left: calc(var(--left) * 100upx - 150upx);
		z-index: var(--index);
	}
	.cu-list.grid.no-border{
		padding: 0 10upx;
	}
	.card-swiper{height: 360upx !important;}
	.card-swiper uni-swiper-item{padding: 20upx 0 100upx;}
</style>
