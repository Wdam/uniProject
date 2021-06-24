<template>
	<view>
	<view class="page-section-spacing">
		<swiper :indicator-dots="true" :autoplay="true" 
		:interval="3000" 
		:duration="1000"
		:circular="true">
			<swiper-item v-for="(item,index) in swiperList" :key='index'>
				<image :src="item.img" mode="aspectFill"></image>
			</swiper-item>
			
		</swiper>
		<!-- 导航 -->
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in navList" :key='index' @click="toNewPage(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
			
			
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">
				推荐商品
			</view>
			<goods-list :goodsList="goodsList"></goods-list>
		</view>
	</view>	
	</view>
</template>

<script>
	import GoodsList from '../../components/GoodsList.vue'
	export default {
		data() {
			return {
				swiperList:[],
				goodsList:[],
				navList:[
					{
						title:'黑马超市',
						icon:'iconfont icon-biaoqiankuozhan_chaoshi-212',
						path:'/pages/hm/hm_chaoshi/hm_chaoshi'
					},
					{
						title:'黑马视频',
						icon:'iconfont icon-shipin font_size',
						path:'/pages/hm/hm_video/hm_video'
					},
					{
						title:'联系我们',
						icon:'iconfont icon-lianxi font_size',
						path:'/pages/hm/contentus/contentus'
					},
					{
						title:'学习图片',
						icon:'iconfont icon-image font_size',
						path:'/pages/hm/hm_img/hm_img'
					},
				]
			}
		},
		components:{
			'goods-list':GoodsList
		},
		onLoad() {
			this.getSwipers()
			this.getgoods()
		},
		methods: {
			//获取轮播图数据
			async getSwipers(){
			const res = await this.$myRequest({
					url:"/api/getlunbo"
				})
				this.swiperList = res.data.message	
			},
			// 获取推荐图
			async getgoods(){
			const res = await this.$myRequest({
					url:"/api/getgoods?pageindex=1"
				})
				this.goodsList = res.data.message	
			},
			toNewPage(url){
				console.log(url)
				uni.navigateTo({
					url
				})
			},
			
		}
	}
</script>

<style lang="less">
	@color : #b50e03;
.page-section-spacing{
	swiper{
		height: 414rpx;
		swiper-item{
			image{
				width: 100%;
				height: 100%;
				
			}
		}
	}
}
.nav{
	display: flex;
	margin-top: 40rpx;
	.nav-item{
		flex: 1;
		text-align: center;
		width: 25%;
		text{
			font-size: 15px;
		}
		view{
			
			width: 120rpx;
			height: 120rpx;
			border-radius: 50%;
			background-color: red;
			margin: 10px auto;
			line-height: 120rpx;
			color: #FFFDEF;
			font-size: 80rpx;
		}
		

		
	}
}
.hot_goods{
	background-color: #eee;
	overflow: hidden;
	margin-top: 10px;
	.tit{
		height: 50px;
		line-height: 50px;
		color: @color;
		text-align: center;
		letter-spacing: 20px;
		background-color: #ffffff;
		margin: 15rpx 0;
		font-size: 25px;
	}
	
}
</style>
