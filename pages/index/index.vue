<template>
	<view class="home">
		<!-- banner -->
		<!-- <image src="../../static/a1.jpg" style="width: 100%;height: 403rpx"></image> -->
		<!-- 1s = 1000ms  interval="2000"-->
		<swiper 
			autoplay="true" 
			interval="2000" 
			indicator-dots="true"
			indicator-active-color="orange"
			class="banner"
		>
			<!-- 一个切换内容 -->
			<swiper-item>
				<image src="../../static/banner2.jpg"></image>
			</swiper-item>
			
			<swiper-item>
				<image src="../../static/banner3.jpg"></image>
			</swiper-item>
			
			<swiper-item>
				<image src="../../static/banner1.jpg"></image>
			</swiper-item>
		</swiper>
		
		<!-- 其它内容：导航，门店等imagee-->
		<!-- 跳转到列表 -->
		<!-- <navigator url="../list/list">
			<image src="../../static/gif/home_static.gif" style="width:100%;height: 2209rpx;"></image>
		</navigator> -->
		
		<!--  写页面：1.分面页面，看成一快快的 2.写结构：选标签 3.样式  -->
		<!-- 导航start -->
		<view class="box nav">
			<!-- 一个导航：外卖点餐 -->
			<view class="nav_item"><!-- 到列表-->
				<navigator url="../list/list">
					<image src="../../static/nav1.gif"></image>
					<text>外卖点餐</text>
				</navigator>
			</view>
			
			<view class="nav_item">
				<image src="../../static/nav2.gif"></image>
				<text>到店自提</text>
			</view>
			<view class="nav_item">
				<image src="../../static/nav3.gif"></image>
				<text>扫码点餐</text>
			</view>
			<view class="nav_item">
				<image src="../../static/nav4.gif"></image>
				<text>快捷付款</text>
			</view>
		</view>
		<!-- 导航end-->
		
		<!-- 饭票 -->
		<!-- class 属性 值可以有多个class,用空格隔开 -->
		<view class="box food">
			<navigator url="../list/list">
				<image src="../../static/fanpiao.gif"></image>
			</navigator>
		</view>
		
		<!-- 门店 -->
		<view class="box shop">
			<view class="title">门店介绍</view>
			<!-- 门店信息 -->
			<view class="info">
				<image src="../../static/door.gif"></image>
				<view class="brand">
					<view class="shop_name">川胖子特色菜馆</view>
					<view class="address">湖北省武汉市洪山区樱花大厦198号</view>
					<view class="time">营业时间：00：00 - 23：00</view>
				</view>
			</view>
			
			<!-- 联系 -->
			<view class="contact">
				<image src="../../static/telephone.png"></image>
				<text>联系商家</text>
				<text class="divider">|</text>
				<image src="../../static/shop_nav.png"></image>
				<text>导航到家</text>
			</view>
	    </view>
			
		<!-- 今日推荐 -->
		<view class="box recomment">
			<view class="title">今日推荐</view>
			<!-- swiper -->
			<swiper 
			class="hot_product" 
			autoplay="ture" 
			interval="2000" 
			indicator-dots="true"
			indicator-active-color="red">
				<swiper-item>
					<image src="../../static/hot_product.gif"></image>
					<view class="info">
						<view class="info_title">油闷大虾</view>
						<!-- .price text:first-child -->
						<view class="price">
							<text>￥</text>
							<text>128</text>
						</view>
						<!-- 使用定位 -->
						<view class="buy">
						  一键下单
						</view>
					</view>
				</swiper-item>
				
				<swiper-item>
					<image src="../../static/hot_product.gif"></image>
					<view class="info">
						<view class="info_title">油闷牛哇</view>
						<!-- .price text:first-child -->
						<view class="price">
							<text>￥</text>
							<text>198</text>
						</view>
						<!-- 使用定位 -->
						<view class="buy">
						  一键下单
						</view>
					</view>
				</swiper-item>
				
				<swiper-item>
					<image src="../../static/hot_product.gif"></image>
					<view class="info">
						<view class="info_title">油闷小虾</view>
						<!-- .price text:first-child -->
						<view class="price">
							<text>￥</text>
							<text>98</text>
						</view>
						<!-- 使用定位 -->
						<view class="buy">
						  一键下单
						</view>
					</view>
				</swiper-item>
				
			</swiper>
		</view>
		
		<!-- 充值卡 -->
		<view class="box charge">
			<view class="title">
				<text>优惠储值</text>
				<text>更多 ></text>
			</view>
			
			<view class="charge_desc">储值返现多，多储多返</view>
			
			<swiper 
			class="charge_info"
			autoplay="true" 
			indicator-dots="true" 
			interval="2600" 
			indicator-active-color="red">
				<!-- 一个切换的内容 -->
				<swiper-item>
					<image src="../../static/zhekou-1.gif" mode=""></image>
					<image src="../../static/zhekou-2.jpg" mode=""></image>
				</swiper-item>
				
				<swiper-item>
					<image src="../../static/zhekou-2.jpg" mode=""></image>
					<image src="../../static/zhekou-1.gif" mode=""></image>
				</swiper-item>
				
			</swiper>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	/* 页面根 */
	.home{
		background-color: #F9F9F9;
		padding-bottom: 10rpx;
	}
	
	/* bannner 图片 */
	.home .banner image{
		height: 403rpx;
		width: 100%;
	}
	
	/* .box 每一块的公用样式：*/
	.box{
		padding: 15rpx;
		margin: 14rpx;
		background-color: #FFFFFF;
		border-radius: 10rpx;
	}
	
	/* 导航 */
	.nav{
		/* 这使用flex布局，就可以该变子元素的排列方式 */
		display: flex;
		/* flex-direction: row; */
		/* 子元素排列方式 */
		justify-content: space-between;
		/* 盒子 与 内容的间距 */
		/* .box */
		/* padding: 15rpx;
		margin: 14rpx;
		background-color: #FFFFFF;
		border-radius: 10rpx; */
	}
	
	/* 图片 */
	.nav .nav_item image{
		width: 93rpx;
		height: 87rpx;
		/* 让img变成块元素，独占1行 */
		display: block;
		/* 图片水平居中 */
		margin: 0 auto;
		margin-bottom: 16rpx;
	}
	
	.nav .nav_item text{
		font-size: 26rpx;
		/* 加粗 */
		/* font-weight: bold; */
	}

    /* 饭票 */
	.food{
		/* padding: 15rpx;
		margin: 14rpx;
		background-color: #FFFFFF;
		border-radius: 10rpx; */
		/* .box */
	}
    .food image{
		width: 100%;
		height: 177rpx;
	}
	
	/* 门店介绍 */
	.shop .title{
		font-size: 33rpx;
		/* 上下 16，左右0 */
		padding: 14rpx 0;
		color: #323232;
		/*加粗 */
		font-weight: bold;
	}
	
	/*  */
	.shop .info{
		display: flex;
		/* 让左右水平排 */
	}
	
	.shop .info > image{
		width: 136rpx;
		height: 140rpx;
		margin-right: 14rpx;
	}
	
	.info .brand .shop_name{
		color: #323232;
		font-weight: bold;
		font-size: 35rpx;
	}
	
	/* 组选择器：多个选择器使用相同的样式，逗号分隔 */
	.brand .address,.brand .time{
		font-size: 26rpx;
	}
	
	.brand .address{
		margin: 4rpx 0;
	}
	
	.brand .time{
		color: #D23C34;
		border: solid 1px #D23C34;
		padding:4rpx;
		/* 转为行内元素，内容有多少，不显示多大 */
		display: inline;
	}
	
	/*  */
	.contact{
		display: flex;
		/* 默认 主轴是x轴 */
		/* 设置交叉轴对齐方式 */
		align-items: center;
		font-size: 16rpx;
		margin-top: 16rpx;
	}
	.contact image{
		width: 32rpx;
		height: 32rpx;
		margin-right: 10rpx;
	}
	
	.contact .divider{
		/* 上下0，左右10 */
		padding: 0 10rpx;
	}
	
	/* 热门产品 标题*/
	.recomment{
		padding-bottom: 30rpx;
	}
	.recomment .title{
		padding: 15rpx 0;
	    font-size: 34rpx;
	}
	
	/* swiper */
	.hot_product{
		height: 858rpx;
		box-shadow: 0 0 10rpx #C0C0C0;
		padding-bottom: 20rpx;
	}
	
	.hot_product swiper-item image{
		height: 718rpx;
		width: 100%;
		/* border-radius:10rpx */
		/* 左上 */
		border-top-left-radius: 20rpx;
		/* 右上 */
        border-top-right-radius: 20rpx;		
		/* 右下 */
		border-bottom-right-radius: 50rpx;
		/* 左下 */
		
	}
	
	/* 产品标题 */
	.hot_product .info{
		/* 使用相对定位，作为子元素使用 决对定位 时的 参照点/参考点 */
		position: relative;
		/* left: 0;
		top: 0; */
		
		padding-bottom: 30rpx;
	}
	.hot_product .info .info_title{
		font-size: 36rpx;
		/* color: red; */
		/* 4个方向分开写：以从上边开始，顺时针旋转：上，右，下，左 */
		padding:15rpx 0 20rpx 15rpx;
	}
	
	/* 价格 */
	.hot_product .info .price{
		color:#C52237;
		padding-left: 15rpx;
	}
	
	/* .price 下面的 第1个 text */
	.price text:first-child{
		font-size: 18rpx;
		/* color: #007AFF; */
	}
	
	.hot_product .info .buy{
		width: 160rpx;
		background-color: #C52237;
		border-radius:120rpx;
		
		padding-top:20rpx;
		padding-right: 30rpx;
		padding-bottom: 20rpx;
		padding-left: 30rpx;
		
		/* 简写: 上下，左右*/
		/* padding:20rpx 30rpx; */
		text-align: center;
		color: #FFFFFF;
		font-size: 32rpx;
		/* 字符间距，文字之间的距离 */
		letter-spacing:4rpx;
	}
	
	.hot_product .info .buy{
		/* 相对它父元素的 绝对定位 */
		position: absolute;
		/* 左上角 */
		/* left: 0;
		top:0 */
		right: 0;
		top:34rpx;
	}
	
	/*充值*/
	.charge{
		padding:20rpx;
	}
	
	/* 1 row */
	.charge .title{
		display: flex;
		/* flex-direction: row; */
		justify-content: space-between;
	}
	
	/* .title 下的第1个 text  */
	.charge .title text:first-child{
		font-size: 34rpx;
		/* color: red; */
	}
	
	/* #a4a4a4 */
	/* .title 下的 最后1个 text  */
	.charge .title text:last-child{
		color: #a4a4a4;
		font-size: 28rpx;
	}
	
	/* 2 row */
	.charge .charge_desc{
		color: #a4a4a4;
		font-size: 30rpx;
		padding:24rpx 0;
		letter-spacing: 2rpx;
	}
	
	/* 3 row */
	.charge_info{
		height: 240rpx;
	}
	/* ctrl + f  */
	.charge .charge_info swiper-item{
		display: flex;
		/* flex-direction: row; */
		/* 两边对其 */
		justify-content: space-between;
	}
	
	.charge .charge_info swiper-item image{
		width: 100%;
		height: 172rpx;
	}
	
	/* 设置 第2个图片的左 外边距 
	  2的倍数的图片
	*/
	.charge .charge_info swiper-item image:nth-child(2n){
		margin-left:20rpx;
	}
	
</style>
