<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view @click="leftClickHandle(index,item.id)" :class="active===index?'active':''" v-for="(item,index) of cates" :key="index">{{item.title}}</view>
		</scroll-view>
		<!-- 右侧数据 -->
		<scroll-view class="right" scroll-y>
			<view class="item" v-for="(item,index) of secondDate" :key="index">
				<image @click="previewImg(item.img_url)" :src="item.img_url"></image>
				<text>{{item.title}}</text>
			</view>
			<text v-if="secondDate.length === 0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:0,
				secondDate:[]
			}
		},
		methods: {
			async getPicsCate() {
				const res = await this.$myRequest({
					url:'/api/getimgcategory'
				})
				this.cates = res.data.message
				this.leftClickHandle(0,this.cates[0].id)
			},
			async leftClickHandle(index,id) {
				this.active = index;
				//获取右侧数据
				const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondDate = res.data.message
			},
			previewImg(current) {
				const urls = this.secondDate.map(item=>{
					return item.img_url
				})
				uni.previewImage({
					current,
					urls
				})
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		height: 100%;
		display: flex;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}	
			.active{
				background: $shop-color;
				color: #fff;
			}
		}
		.right{
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;
			.item{
				image{
					width: 520rpx;
					height: 520rpx;
					border-radius: 5px;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}
</style>
