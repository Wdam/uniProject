<template>
	<view class="contact">
		<map class="map"
			:latitude="latitude"
			:longitude="longitude"
			scale="11" 
			:markers="markers"
			:show-location="true"
			@markertap="markertap"
			@updated='mapUpdated'
			@tap='closeMapMarker'></map>
	
	</view>
</template>

<script>
	import amap from '../../../js_sdk/AMapWX_SDK_V1.2.1/amap-wx.js'
	export default {
		data() {
			return {
				longitude:0,
				latitude:0,
				mapkey:'b6632ca4eea880322607c3f6a2ea43a9',
				
			}
		},
		onLoad() {
			this.getLocal()
		},
		methods: {
			getLocal(){
				const that = this
				that.amapPlugin = new amap.AMapWX({
					key:that.mapkey
				});
				that.amapPlugin.getRegeo({
					type:'gcj02',
					success:(res) =>{
						console.log(res)
						const {latitude ,longitude } = res[0]
						that.longitude = longitude;
						that.latitude = latitude;
						that.mapInfo=res[0];
					}
				})
			}
		}
	}
</script>

<style lang="less">
.map{
	width: 750rpx;
	height: 750rpx;
}
</style>
