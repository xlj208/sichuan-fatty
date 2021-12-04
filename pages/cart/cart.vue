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
		<!-- 无商品时显示 -->
		<view  v-if="cart_info.totalNum ==0" style="text-align: center;">暂无商品!</view>
		
		<!-- 3.使用 v-for,v-bind指令显示数据 -->
		<!-- 1个产品 -->
		<view class="item" v-for="val in cart_info.pro_list">
			<!-- 左 -->
			<view class="item_left">
				<navigator :url="'../detail/detail?id='+val.id">
					<image :src="val.pic"></image>
				</navigator>
				<view>
					<view class="title">{{val.title}}</view>
					<view class="price">￥{{val.price}}.0</view>
				</view>
			</view>
			<!-- 无商品时显示 -->
			<!-- <text v-if="cart_info.product.length == 0" style="text-align: center;">暂无商品!</text> -->
			
			<!-- 右边 -->
			<!--  跳转到菜单页面，加 open-type="switchTab"-->
			<!-- <navigator url="../cart/cart" open-type="switchTab"> -->
			<view class="item_right">
				<text>￥{{val.num * val.price}}.0</text>
				<image src="../../static/reduce_pro.png" mode="" @click="reduceCart(val.id)"></image>
				<text> {{val.num}} </text>
				<image  src="../../static/add_pro.png" mode="" @click="addCart(val.id)"></image>
			</view>
		</view>
		<!-- 1个产品 -->
		
		<!-- 统计信息 -->
		<view class="cart_info" v-if="cart_info.totalNum >0">
			<text>总数：{{cart_info.totalNum}}</text>
			<text>总价：<text>￥{{cart_info.totalPrice}}.0</text></text>
		</view>
	</view>
</template>

<!-- 2.script js,实现功能 -->
<script>
	export default {
		data() {
			return {
				cart_info:{} //购物车数据
			}
		},
		methods: {
			// 加
			addCart(id){
				// 1.获取id
				console.log("添加id:",id)
				// 2.获取产品，
				var list = this.cart_info.pro_list;//产品列表
				console.log(list);
				// 3.找到 id 对应的产品，修改数量
				for(var k=0;k<list.length;k++){
					if(list[k].id == id){
						console.log("找到了当前产品:",list[k]);
						// 数量+1
						list[k].num = list[k].num+1;
						break;//跳出循环
					}
				}
				console.log("更新后的产品列表:",list);
				
				//4.更新：总数，总价
				var totalNum = 0;
				var totalPrice=0;
				for(var k=0;k<list.length;k++){
					totalNum = totalNum + list[k].num;
					totalPrice = totalPrice + (list[k].num * list[k].price);
				}
				console.log("总数，总价",totalNum,totalPrice);
				
				//5.修改后的购物车数据
				var cart_info = {
					pro_list:list,
					totalNum:totalNum,
					totalPrice:totalPrice
				}
				//6.同步到页面
				this.cart_info = cart_info;
				//7.保存起来
				uni.setStorage({
					key:"my_cart",
					data:cart_info,
					fail() {
						console.log("保存失败")
					},
					success() {
						console.log("保存ok")
					}
				})
				
			},
			reduceCart(id){
				// 1.获取id
				console.log("添加id:",id)
				// 2.获取产品，
				var list = this.cart_info.pro_list;//产品列表
				console.log(list);
				// 3.找到 id 对应的产品，修改数量
				for(var k=0;k<list.length;k++){
					if(list[k].id == id){
						console.log("找到了当前产品:",list[k]);
						// 数量-1
						if(list[k].num-1 <=0){
							// list[k].num =1;//最少为1件商品
							list.splice(k,1); //当只有 1件商品的时候，从购物车中删除
							//提示信息
							uni.showToast({
								title:'删除成功!'
							})
							// arr.spclice(index,n) 从数组的指定下标中删除 n 个元素
						}else{
							list[k].num = list[k].num-1;
						}
						break;//跳出循环
					}
				}
				console.log("更新后的产品列表:",list);
				
				//4.更新：总数，总价
				var totalNum = 0;
				var totalPrice=0;
				for(var k=0;k<list.length;k++){
					totalNum = totalNum + list[k].num;
					totalPrice = totalPrice + (list[k].num * list[k].price);
				}
				console.log("总数，总价",totalNum,totalPrice);
				
				//5.修改后的购物车数据
				var cart_info = {
					pro_list:list,
					totalNum:totalNum,
					totalPrice:totalPrice
				}
				//6.同步到页面
				this.cart_info = cart_info;
				//7.保存起来
				uni.setStorage({
					key:"my_cart",
					data:cart_info,
					fail() {
						console.log("保存失败")
					},
					success() {
						console.log("保存ok")
					}
				})
				
			}
		},
		onShow() {
			// 1.当页面显示的时候，自动执行-->获取购物车的数据
			console.log("获取购物车的数据");//"获取购物车的数据" ,'aa','a'
			var _this = this;//保存当前组件 this
			
			uni.getStorage({
				key:"my_cart",
				fail() {
					console.log('购物车中没有商品')
					_this.cart_info = [];
				},
				success(ret){
					console.log("获取到了数据:",ret.data)
					// 2.保存到变量中，显示，操作
					_this.cart_info = ret.data;
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
		width: 100%;
		/* position: fixed; */
		/* 网页尺寸 */
		/* bottom: 130rpx; */
		/* 小程序尺寸 */
		/* bottom: 30rpx; */
		margin-right: 10rpx;
	}
	
	.cart_info text:first-child{
		margin-right: 30rpx;
	}
	
	/* nth-child(n) 选择第 n (1,2,...n) 个子元素，第2个 text*/
	.cart_info text:nth-child(2){
		color:orange;
	}
</style>
