<template>
		<view class="pics">
			<scroll-view class="left" scroll-y="true">
				<view 
				:class="active === index? 'active':' '"
				v-for="(item,index) in titleList" :key="index"
				@click="changeIndex(index,item.id)">
					{{item.title}}
				</view>
			</scroll-view>
			<scroll-view scroll-y="true" class="right">
				<view class="item" v-for="(item,id) in secondData" :key="id">
					<image src="../../../static/phone.jpg" mode=""></image>
					<text>{{item.title}}</text>
				</view>

			</scroll-view>
		</view>
	
</template>

<script>
	export default {
		data() {
			return {
			titleList:[],
			active:0,
			secondData:[]
			}
		},
		onLoad() {
			this.getPics();
			
			
		},
		// onLoad: () => {
			
		// }
		methods: {
		async getPics(){
		
		const res =	await this.$myRequest({
					url:'/api/getimgcategory'
				})
				
				this.titleList = res.data.message
			},
		async changeIndex(index,id){
				this.active = index
			const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondData  = res.data.message
			}
				
			
		}
	}
</script>

<style lang="less">
page{
		height: 100%;
	}
.pics{
	height: 100%;
	display: flex;
	background-color: #b4b3b3;
		.left{
			width: 200rpx;
			height: 100%;
			background-color:  pink;
			border-right: 1px solid #000000
		}
		view{
			height: 60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top: 1px solid #000000;
		}
		.active{
			background-color: red;
			color: #FFFFFF;
		}
		.right{
			height: 100%;
			width: 530rpx;
			margin: 10rpx auto;
			.item{
				height: 70%;
				image{
					width: 530rpx;
					height: 530rpx;
					border-radius: 5rpx;
					background-color: pink;
					}
				text{
					font-size: 40rpx;
					line-height: 30rpx;
				}
			}
		}
}
</style>
