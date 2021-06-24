<template>
	<view>
		<view class="goods_list">
			<view class="goods_item" v-for="item in goodsList" :key='item.id'>
				<image src="../static/phone.jpg" mode=""></image>
				<view class="price">
					<text>￥{{item.sell_price}}</text>
					<text>￥{{item.market_price}}</text>
				</view>
				<view class="title">
					{{item.title}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"GoodsListr",
		props:['goodsList'],
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="less">
	@color : #b50e03;
.goods_list{
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.goods_item{
			margin: 10rpx 0;
			background-color: #FFFFFF;
			width: 355rpx;
			padding: 15rpx;
			box-sizing: border-box;
			image{
				display: block;
				width: 70%;
				height: 150px;
				margin: 0 auto;
			}
		}
		.price{
			color: @color;
			font-size: 40rpx;
			text:nth-child(2){
				margin-left: 10rpx;
				color: pink;
				font-size: 20rpx;
				text-decoration: line-through;
			}
		}
		.title{
			font-size: 28rpx;
			line-height: 50rpx;
			padding-bottom: 15rpx;
			padding-top: 10rpx;
		}
	}
</style>
