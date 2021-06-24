<template>
	<view class="goods_list">
		<goods-list :goodsList="goodsList"></goods-list>
		<view class="buttom" v-if="flag">
			<text>------到底了------</text>
		</view>
	</view>
</template>

<script>
	import GoodsList from '../../../components/GoodsList.vue'
	export default {
		data() {
			return {
				pageindex:1,
				goodsList:[],
				flag:false
			}
		},
		components:{'goods-list':GoodsList},
		onLoad() {
			this.getgoods()
		},
		methods: {
			// 获取推荐图
			async getgoods(callBack){
			const res = await this.$myRequest({
					url:`/api/getgoods?pageindex=${this.pageindex}`
				})
				this.goodsList = [...this.goodsList,...res.data.message]
				callBack && callBack()
			},
			onReachBottom(){
				if(this.goodsList.length<this.pageindex*10) return this.flag = true
				this.pageindex++
				console.log(this.pageindex)
				this.getgoods()
			},
			onPullDownRefresh(){
				this.pageindex=1,
				this.goodsList=[],
				this.flag=false,
				setTimeout(() =>{
					this.getgoods(() =>{
							uni.stopPullDownRefresh()
					})
				},1000)
			}
		}
	}
</script>

<style lang="less">
.goods_list{
	background-color: #EEEEEE;
	.buttom{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		
		font-size: 10px;
	}
}

</style>
