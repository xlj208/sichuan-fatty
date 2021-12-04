<!-- 
x.vue 看成是一个html文件,就是一个页面,一个页面也可以看 成是一个组件
页面结构:
 1.template  内容,各种标签
    下面必须要有一个根标签,不能有2个子元素
 2.script js,实现功能
 3.style
 -->
<template>
	<!-- 给 view标签 定义一个样式 -->
	<view class="list">
		<!-- 1个产品 -->
		<view class="item">
			<!-- 左 -->
			<view class="item_left">
				<navigator url="../detail/detail?id=1">
					<image src="../../static/upload/list1.jpg"></image>
				</navigator>
				<view>
					<view class="title">特色烤鱼</view>
					<view class="price">￥98.0</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥19.0</text>
				<image src="../../static/reduce_pro.png" mode=""></image>
				<text>1</text>
				<image  src="../../static/add_pro.png" mode=""></image>
			</view>
		</view>
		
		<!-- 1个产品 -->
		<view class="item">
			<!-- 左 -->
			<view class="item_left">
				<navigator url="../detail/detail?id=2">
					<image src="../../static/upload/list1.jpg"></image>
				</navigator>
				<view>
					<view class="title">特色烤鱼</view>
					<view class="price">￥98.0</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥19.0</text>
				<image src="../../static/reduce_pro.png" mode=""></image>
				<text>1</text>
				<image  src="../../static/add_pro.png" mode=""></image>
			</view>
		</view>
		
		<!-- 1个产品 -->
		<view class="item">
			<!-- 左 -->
			<view class="item_left">
				<navigator url="../detail/detail">
					<image src="../../static/upload/list1.jpg"></image>
				</navigator>
				<view>
					<view class="title">特色烤鱼</view>
					<view class="price">￥98.0</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥19.0</text>
				<image src="../../static/reduce_pro.png" mode=""></image>
				<text>1</text>
				<image  src="../../static/add_pro.png" mode=""></image>
			</view>
		</view>
		
		<!-- 1个产品 -->
		<view class="item">
			<!-- 左 -->
			<view class="item_left">
				<navigator url="../detail/detail">
					<image src="../../static/upload/list1.jpg"></image>
				</navigator>
				<view>
					<view class="title">特色烤鱼</view>
					<view class="price">￥98.0</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥19.0</text>
				<image src="../../static/reduce_pro.png" mode=""></image>
				<text>1</text>
				<image  src="../../static/add_pro.png" mode=""></image>
			</view>
		</view>
		
		<!-- 1个产品 -->
		<view class="item">
			<!-- 左 -->
			<view class="item_left">
				<navigator url="../detail/detail">
					<image src="../../static/upload/list1.jpg"></image>
				</navigator>
				<view>
					<view class="title">特色烤鱼</view>
					<view class="price">￥98.0</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥19.0</text>
				<image src="../../static/reduce_pro.png" mode=""></image>
				<text>1</text>
				<image  src="../../static/add_pro.png" mode=""></image>
			</view>
		</view>
	    
		<view class="cart_info">
			<text>总数：5</text>
			<text>总价：<text>￥95.0</text></text>
		</view>	
		
	</view>
</template>

<!-- 2.script js,实现功能 -->
<script>
	export default {
		data() {
			return {
				num: 100, //页面的数据
				age: 20,
				product:[]
			}
		},
		methods: {

		},
	}
</script>

<!-- 3.样式 -->
<style>
	.list{
		padding: 16rpx;
	}
	
	/* 一个产品 最大的盒子 */
	.item{
		/* 添加相对定位，作为子元素 绝对定位时候的参考点 */
		/* position: relative; */
		/* left:0;
		top:0; */
		margin-bottom: 16rpx;
		display: flex;
		justify-content: space-between;
	}
	/* 大图 */
	.item .item_left image{
		width: 173rpx;
		height: 173rpx;
		margin-right: 16rpx;
	}
	
	/* 水平排列 */
	.item .item_left{
		display: flex;
		/* flex-direction: row; */
	}
	
	.item .item_left .title{
		/* 加粗 */
		font-weight: bold;
		font-size: 34rpx;
	}
	
	/* 组选择器：相同样式的选择放一起，使用 逗号(,)分割*/
	.item .item_left .tongji,
	.item .item_left .time,
	.item .item_left .price{
		color: #928688;
	}
	
	.item .item_left .tongji,
	.item .item_left .time{
		font-size:28rpx;
	}
	
	.item .item_left .price{
		font-size: 30rpx;
		margin-top: 40rpx;
		color:orange
	}
	/* add */
	.item .item_right{
		display: flex;
		/* 水平 分散 对齐 */
		justify-content: space-around;
		/* 垂直 剧中 对齐 */
		align-items: center;
	}
	.item .item_right image{
		width: 64rpx;
		height: 64rpx;
		
	}
	
	/* bottome */
	.cart_info{
		display: flex;
		flex-direction: row;
		/* 从 右 到 左 */
		/* justify-content: flex-start; */
		justify-content: flex-end;
	}
	
	.cart_info text:first-child{
		margin-right: 16rpx;
	}
	
	/* nth-child(n) 选择第 n (1,2,...n) 个子元素，第2个 text*/
	.cart_info text:nth-child(2) text{
		color: #F54745;
	}
</style>
