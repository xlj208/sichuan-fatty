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
		<!-- 1个产品 start -->
		<view class="item" v-for="val in pro_list">
			<!-- 左 -->
			<view class="item_left">
				<!-- <navigator url="../detail/detail?id=1"> -->
				<navigator v-bind:url="'../detail/detail?id='+val.id">
					<!-- <image src="../../static/upload/list1.jpg"></image> -->
					<image :src="val.pic"></image>
				</navigator>
				<view>
					<view class="title">{{val.title}}</view>
					<view class="tongji">
						<text>月售 {{val.sale}}</text>
						<text>点赞{{val.support}}</text>
					</view>
					<view class="time">备货时间{{val.prepare_time}}钟</view>
					<view class="price">￥{{val.price.toFixed(1)}}/份</view>
				</view>
			</view>
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<navigator url="../detail/detail?id=1" open-type="navigate">
				<image class="item_right" src="../../static/add_pro.png" mode=""></image>
			</navigator>
		</view>
		<!-- 1个产品 end-->
		
		<!-- <ul>
			<li v-for="val in pro_list">{{val.id}}-{{val.title}}</li>
		</ul> -->
	</view>
</template>

<!-- 2.script js,实现功能 -->
<script>
	var id =1;
	var str = '../detail/detail?id='+id
	console.log(str)
	
	export default {
		data() {
			return {
				pro_list:[] //产品列表
			}
		},
		methods: {

		},
		//vue 生命周期钩子函数
		created(){
			console.log('vue 对象 创建完成')
		},
		mounted(){
			//发请求
			console.log('vue 页面挂载完成')
		},
		//uniapp扩展的几个生命周期
		onShow() {
			var _this = this;//保存当前this（组件实例）
			//发请求-推荐
			console.log("页面显示的时候")
			// 语法类似 jQuery $.ajax({...})
			uni.request({
				url:'http://api.brqc.com.cn/list.php',//请求的地址
				data:{}, //参数
				method:"get",
				success(response) {
					//请求成功，服务器返回了结果(response)，自动调用
					console.log('success:',response)
					//真正的数据是在 response.data
					var result_data = response.data || [];
					//取列表
					console.log(result_data,result_data.data)
					if(result_data.code == 0){
						console.log('nice',this)
						//保存产品列表数据，页面好用
						//this 指向的是 success,需要拿到当前组建的this
						// this.pro_list = result_data.data;
						_this.pro_list = result_data.data;
					}
				},
				fail(response) {
					//请求不成功，服务器返回了结果(response)，自动调用
					console.log('error',response)
				},
				complete(response) {
					// console.log('complete:',response)
				}
			})
		}
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
		position: relative;
		/* left:0;
		top:0; */
		margin-bottom: 16rpx;
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
	.item .item_left .tongji text:first-child{
		margin-right: 20rpx;
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
		font-size: 26rpx;
		margin-top: 20rpx;;
	}
	/* add */
	
	.item .item_right{
		width: 64rpx;
		height: 64rpx;
		position: absolute;
		/* left:0;
		top:0 */
		bottom: 0;
		right: 0;
	}
</style>
