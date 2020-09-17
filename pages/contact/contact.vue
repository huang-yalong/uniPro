<template>
	<view class="contact">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：18937817057(点击拨打)</view>
			<view>公司地址：河南省开封市尉氏县大营镇</view>
		</view>
		<map class="map" :longitude="longitude" :scale="scale" :latitude="latitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:114.063204,
				latitude:34.467196,
				scale:13,
				markers:[
					{
						longitude:114.063204,
						latitude:34.467196,
						iconPath:'../../static/log.png',
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber:'400-618-9090'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact{
		.img{
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view{
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map{
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
