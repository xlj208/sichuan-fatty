<template>
	<!-- 页面根元素 -->
	<view>
		<!-- 4.显示数据 -->
		<!-- product -->
		<!-- <image src="../../static/gif/pro_ad.jpg" style="width: 100%;height: 721rpx;"></image> -->
		<image :src="product.pic" style="width: 100%;height: 721rpx;"></image>
		<!-- ctrl + enter 光标到下一行 -->
		<!-- <image src="../../static/gif/pro_add.jpg" style="width: 100%;height: 194rpx;"></image> -->
		<!-- 产品标题，价格，加入购物购物车 -->
		<view class="pro_operate">
			<view class="title">{{product.title}}</view>
			<view class="desc">暂无商品描述</view>
			<view class="pro_btn">
				<!-- left -->
				<view class="price">
					<text>￥</text>
					<text>{{product.price ? product.price.toFixed(1):0.0}}</text>
					<text>/份</text>
				</view>
				<!-- right -->
				<view class="cart_btn" @click="addCart">
					加入购物车
					<view>{{proTotalNum}}</view>
				</view>
			</view>
		</view>

		<!-- 详细 -->
		<image src="../../static/gif/pro_detail.jpg" style="width: 100%;height: 368rpx;padding-bottom: 120rpx;"></image>

		<!-- 底部 -->
		<!-- <image src="../../static/gif/pro_bottom.jpg" style="width: 100%;height:96rpx;"></image> -->
		<view class="pro_bottom">
			<navigator url="../cart/cart" open-type="switchTab">
				<view class="cart">
					<image src="../../static/tabbar/cart.png"></image>
					<view>
						<!-- <view>￥{{cartTotalPrice}}</view> -->
						<view>{{cartTotalPrice|currency}}</view><!-- 使用过滤器 -->
						<view class="express">运费￥3 | 支持自提</view>
					</view>
					<view class="cart_num">{{cartTotalNum?cartTotalNum:0}}</view>
				</view>
			</navigator>
			<view class="require_good">必选商品</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//如果没有动态获取，先把产品信息写死
				//产品信息
				product: {
					/* id: 1,
					pic: "http://api.brqc.com.cn/img/list1.jpg",
					prepare_time: 20,
					price: 19,
					sale: 100,
					support: 200,
					title: "特色烤鱼" */
				}, //id 对应的产品信息
				cartTotalNum:0, //购物车总数
				cartTotalPrice:0,//购物车总价
				proTotalNum:0,//当前产品在购物车中的总数
				pro_id:0
				
			}
		},
		methods: {
			//加入购物车
			addCart(){
				//1.获取到要加入购物车的产品信息
				var pro = this.product;
				console.log(pro)
				//2.加入购物车
				// 思路：
				//2.1 获取购物车
				//2.2 判断购物是否存在
				//2.2.1 如果购物车存在，查询当前产品是否在购物车中
					//A:如果产品在购物车中，修改产品数量
					//B:如果产品不在购物车中，直接把产品加入到购物中
				//2.3 如果购物车 不存在，直接创建一个空的购物车，然后把产品放进去
				//2.4 保存购物到Storage
				
				// start
				//2.1 获取购物车
				uni.getStorage({
					key:'my_cart',
					fail:function(data) {
						//2.2.3购物车不存在
						console.log("购物车不存在",data)
						// 
						//创建一个空的购物车结构，是一个对象(对象里面可以放很多数据)
						var cart = {
							//产品列表,他是一个json数组，数组中的每个json对象代表一个产品信息:{...}
							pro_list:[
								// {...},{...},{...}
							],
							totalNum:0 ,//总数
							totalPrice:0//总价格
						}
						
						//把当前产品加入到购物车里面
						pro.num = 1;//产品数量
						console.log(pro)
						cart.pro_list.push(pro);//向数组添加一个元素
						console.log(cart)
						// 不存在,总数总价
						cart.totalNum=pro.num;
						cart.totalPrice=pro.price;
						//保存到起来
						uni.setStorage({
							key:'my_cart',
							data:cart,
							success:function(data){
								console.log('1-success:',data)
							},
							fail:function(data){
								console.log('1-fail:',data)
							}
						})
						// 
					},
					success:function(result){
						//2.2.1 购物车存在
						console.log("购物车存在，获取成功!",result)
						//从storage中取到的 购物车数据
						var shop_cart = result.data; 
						console.log(shop_cart)
						//判断当前产品是否在 购物车中
						var product = shop_cart.pro_list;//购物车中的产品数组
						var exits = false; //记录当前产品是否在购物车中，false-不在，true-存在
						//拿 当前产品的id 跟 产品数组中的每个元素(产品对象)进行对比，如果id相同，就说明存在
						for(var i=0;i<product.length;i++){
							console.log(product[i])//每个产品对象
							if(pro.id == product[i].id){
								exits = true;
								break; //找到跳出循环
							}
						}
						console.log("产品是否存在:",exits)
						//A:如果产品在购物车中，修改产品数量
						//B:如果产品不在购物车中，直接把产品加入到购物中
						if(exits){
							console.log("修改前：",shop_cart)
							for(var k=0;k<product.length;k++){
								if(pro.id == product[k].id){
									product[k].num = product[k].num+1;
									break;
									
								}
							}
							shop_cart.pro_list = product;
							
						}else{
							pro.num = 1;
							product.push(pro);
							shop_cart.pro_list=product;
							// uni.setStorage({
							// 	key:'my_cart',
							// 	data:shop_cart,
							// 	success:function(data){
							// 		console.log("新的商品，添加完成！")
							// 	}
							// })
						}
						// 存到storage
						console.log("保存前的数据:",shop_cart)
						// 产品列表
						var product_list = shop_cart.pro_list;
						var totalNum = 0;
						var totalPrice = 0;
						for(var m=0;m<product_list.length;m++){
							console.log(product_list[m])
							totalNum = totalNum+product_list[m].num;
							totalPrice = totalPrice+(product_list[m].num*product_list[m].price);
						}
						console.log("总数是："+totalNum)
						console.log("总价是："+totalPrice)
						shop_cart.totalNum=totalNum;
						shop_cart.totalPrice=totalPrice;
						uni.setStorage({
								key:'my_cart',
								data:shop_cart,
								success:function(data){
									console.log("更新购物车完成！",data)
								}
							})
					}
				})
				
				/* //创建一个空的购物车结构，是一个对象(对象里面可以放很多数据)
				var cart = {
					//产品列表,他是一个json数组，数组中的每个json对象代表一个产品信息:{...}
					pro_list:[
						// {...},{...},{...}
					],
					totalNum:0 ,//总数
					totalPrice:0//总价格
				}
				
				//把当前产品加入到购物车里面
				pro.num = 1;//产品数量
				console.log(pro)
				cart.pro_list.push(pro);//向数组添加一个元素
				console.log(cart)
				
				//保存到起来
				uni.setStorage({
					key:'my_cart',
					data:cart,
					success:function(data){
						console.log('success:',data)
					},
					fail:function(data){
						console.log('fail:',data)
					}
				}) */
				this.getCartInfo();
				
			},
			getCartInfo(){
				// 获取购物车
				console.log("获取购物车的信息")
				var _this = this;
				uni.getStorage({
					key:'my_cart',
					success:function(result){
						console.log("购物车————>",result)
						var cart = result.data;
						_this.cartTotalNum = cart.totalNum;
						_this.cartTotalPrice = cart.totalPrice;
						
						//找到 当前产品id 对应的产品对象，然后取他 在购物车中的 总数
						var list = cart.pro_list;//产品列表
						console.log(_this.pro_id,list)
						//返回符合条件的数组元素(产品对象)
						// var current_pro = list.filter(function(item){
						// 	return item.id == _this.pro_id;
						// })
						//_this.proTotalNum = current_pro[0]? current_pro[0].num :0;//保存
						// 用for
						var current_pro=0;
						for(var i=0;i<list.length;i++){
							if(list[i].id == _this.pro_id){
								 current_pro = list[i];//取到当前产品对象
							}
						}
						// console.log(current_pro,current_pro[0].num)
						_this.proTotalNum = current_pro? current_pro.num :0;//保存
					}
				})
			}
		},
		onShow(){
			// 当页面显示,获取购物车信息
			this.getCartInfo()
		},
		filters:{
			//格式化数据(过滤器)
			// {{数据|currency}}使用方法
			currency(val){
				return "￥"+val.toFixed(1);
			}
		},
		onLoad(data) {
			var _this = this;
			// 如果id不存在，直接跳到列表页面
			// /pages/detail/detail?id=1
			//接收url中的查询参数:{id: "1"}
			console.log(data, data.id)
			// 保存 产品id
			this.pro_id=data.id;
			
			if(!data.id){
				uni.navigateTo({
					url:'../list/list'
				})
			}
			//根据id取商品的详细信息
			//http://api.brqc.com.cn/detail.php/1
			uni.request({
				url: 'http://api.brqc.com.cn/detail.php/' + data.id,
				data: {},
				method: "get",
				success(response) {
					console.log("success:", response) //成功
					/* 
					 {
					 	"data": {
					 		"id": 1,
					 		"pic": "http://api.brqc.com.cn/img/list1.jpg",
					 		"title": "特色烤鱼",
					 		"sale": 100,
					 		"support": 98,
					 		"prepare_time": 30,
					 		"price": 68
					 	},
					 	"code": 0, 0成功，-1没有这个产品
					 	"msg": "获取产品信息完成"
					 }
					 */
					var result = response.data; //后端 返回的内容
					// console.log(result.data) //产品信息
					_this.product = result.data; //保存产品信息
					// console.log(_this.product)
				},
				fail(response) {
					console.log("success:", response) //失败
				}
			});
		    //uni.setStorage
			// localStorage
			//保存数据
			/* uni.setStorage({
				key:'username',//保存的名称
				// data:'jack', //内容-js普通类型：字符串，数字
				data:[{id:1,'title':'烤鱼'}],//保存json数组
				success:function() {
					//成功时候调用
					console.log('save success')
				},
				fail:function(){
					//保存失败
					console.log('保存失败')
				},
				complete:function(){
					console.log('操作完成')
				}
			}) */
			// 获取数据
			// uni.getStorage({
			// 	key:"username",
			// 	success:function(data){
			// 		//data 获取到的数据
			// 		console.log('getStorage---》:',data)
			// 	},
			// 	fail:function(data){
			// 		console.log('fail:',data)
			// 	}
			// })
		}
	}
</script>

<style>
	.pro_operate {
		padding: 16rpx;

	}

	/* title */
	.pro_operate .title {
		font-weight: bold;
	}

	/* description */
	.pro_operate .desc {
		font-size: 30rpx;
		color: #C0C0C0;
		/* 上下，左右 */
		padding: 20rpx 0;
	}

	/* add button */
	.pro_operate .pro_btn {
		display: flex;
		justify-content: space-between;
		/* 给一个定位属性，作子元素 使用绝对定位是的 参考点 */
		position: relative;
	}

	/*价格*/
	.pro_btn .price text:first-child {
		color: rgb(249,60,94);
		
	}

	.pro_btn .price text:nth-child(2) {
		font-size: 50rpx;
		/* color: orange; */
		color: rgb(249,60,94);
	}

	.pro_operate .pro_btn .cart_btn {
		background-color: #F93C5E;
		border-radius: 20rpx;
		color: #FFFFFF;
		padding: 20rpx;
		font-size: 26rpx;
	}

	.pro_operate .pro_btn .cart_btn view {
		position: absolute;
		right: 10rpx;
		top: -36rpx;
		background-color: orange;
		/* 圆角 */
		width: 50rpx;
		height: 50rpx;
		border-radius: 50%;
		/* 文字水平剧中 */
		text-align: center;
		/* 文字垂直剧中：line-height:高度*/
		line-height: 50rpx;
	}

	/* 底部:流式布局 */
	.pro_bottom {
		/* display: flex; */
		width: 100%;
		position: fixed;
		left: 0;
		bottom: 0;
	}

	.pro_bottom image {
		width: 64rpx;
		height: 64rpx;
		margin-right: 30rpx;
	}

	.pro_bottom .cart {
		box-sizing: border-box;
		width: 66.6666%;
		float: left;
		display: flex;
		align-items: center;
		font-size: 30rpx;
		background-color: #252C32;
		color: #F9F9F9;
		position: relative;
		padding: 24rpx
	}

	.pro_bottom .cart_num {
		position: absolute;
		left: 60rpx;
		top: -2rpx;
		background-color: orange;
		text-align: center;
		height: 40rpx;
		width: 40rpx;
		border-radius: 50%;
		line-height: 40rpx;
		padding: 6rpx;
		font-size: 28rpx;
	}

	.pro_bottom .cart .express {
		font-size: 22rpx;
		color: #F1F1F1;
	}

	.pro_bottom .require_good {
		width: 33.3333%;
		float: left;
		/* flex: 1; */
		background-color: #F93C5E;
		font-size: 30rpx;
		text-align: center;
		height: 112rpx;
		line-height: 112rpx;
		color: #FFFFFF;
		letter-spacing: 4rpx;
	}
</style>
