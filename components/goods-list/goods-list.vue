<template>
	<view class="goods_list">
		<view class="goods_item" v-for="(item,index) of goods" :key="index" @click="navigator(item.id)">
			<image :src="item.img_url"></image>
			<view class="price">
				<text>￥{{item.sell_price}}</text>
				<text>￥{{item.market_price}}</text>
			</view>
			<view class="name">
				{{item.title}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['goods'],
		methods:{
			navigator(id) {
				this.$emit('goodsItemClick',id)
			}
		}
	}
</script>

<style lang="scss">
	.goods_list{
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		.goods_item{
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;
			background: #fff;
			width: 355rpx;
			image{
				width: 80%;
				height: 150px;
				display: block;
				margin: auto;
			}
		}
		.price{
			margin: 20rpx 0 5rpx 0;
			color: $shop-color;
			font-size: 36rpx;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				margin-left: 20rpx;
				text-decoration: line-through;
			}
		}
		.name{
			font-size: 28rpx;
			line-height: 50rpx;
			padding-bottom: 15rpx;
			padding-top: 10rpx;
		}
	}
</style>
