<template>
	<view class="me">
		<view class="head">
			<p class="img">
				<image src="../../static/me_1.png"></image>
			</p>

			<a>登录/绑定/注册</a>
		</view>
		<view class="discounts">
			<ul>
				<li>
					<a href="#">
						<span>0</span>
						<p>储值充值</p>
					</a>
				</li>
				<li>
					<a href="#">
						<span>0</span>
						<p>我的饭票</p>
					</a>
				</li>
				<li>
					<a href="#">
						<span>0</span>
						<p>优惠卷</p>
					</a>
				</li>
				<li>
					<a href="#">
						<span>0</span>
						<p>积分商城</p>
					</a>
				</li>
			</ul>
		</view>

		<view class="function">
			<h2>我的功能</h2>
			<ul>
				<li>
					<a href="#">
						<image src="../../static/w_1.png"></image>
						<p>收货地址</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_2.png"></image>
						<p>订单评价</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_3.png"></image>
						<p>买单记录</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_4.png"></image>
						<p>优惠卷兑换</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_5.png"></image>
						<p>拼团记录</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_6.png"></image>
						<p>秒杀记录</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_7.png"></image>
						<p>砍价记录</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_8.png"></image>
						<p>折扣卷记录</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_9.png"></image>
						<p>门店推广员</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_10.png"></image>
						<p>收藏我们</p>
					</a>
				</li>
			</ul>
		</view>

		<view class="serve">
			<h2>我的服务</h2>
			<ul>
				<li>
					<a href="#">
						<image src="../../static/w_11.png"></image>
						<p>帮助与反馈</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_12.png"></image>
						<p>我要开店</p>
					</a>
				</li>
				<li>
					<a href="#">
						<image src="../../static/w_13.png"></image>
						<p>我要合作</p>
					</a>
				</li>
			</ul>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>


<style lang="less">
	page{
		background-color: #f9f9fb;
	}
	.me {
		// background-color: #f9f9fb;
		height: 100%;
		width: 100%;
		
		
		// 登录
		view {
			&.head {
				display: flex;
				padding: 56rpx 0 27rpx 27rpx;
				background: -webkit-linear-gradient(top,#18B7f9,#f9f9fb);
				p {
					&.img {
						width: 130rpx;
						height: 130rpx;
						text-align: center;
						border-radius: 100rpx;
						
						image {
							margin: 0 auto;
							width: 117rpx;
							height: 114rpx;
						}
					}
				}


				a {
					margin: 34rpx 17rpx;
					font-size: 28rpx;
					font-weight: bold;
				}
			}
		}
		
		// 优惠卷
		view {
			&.discounts {
				/* background-color: red; */
				margin: -30rpx 30rpx 0 30rpx;

				ul {
					/* ul 默认边距 */
					/* padding-left: 0; */
					display: flex;
					background-color: #FFFFFF;
					margin: 0 auto;
					/* flex-direction: row; */
					justify-content: space-between;
					/* padding-top: 12rpx; */
					padding: 40rpx;
					border-radius: 14rpx;

					li {
						list-style: none;
						/* 文字，图片居中 */
						text-align: center;

						a {
							text-decoration: none;
							color: #505050;
							font-weight: bold;

							span {
								font-size: 30rpx;
								color: #efc173;
							}

							p {
								margin-top: 20rpx;
								font-size: 22rpx;
							}
						}
					}
				}
			}

		}

		// 我的功能
		view {
			&.function {
				margin: 20rpx 25rpx;
				background-color: #FFFFFF;
				border-radius: 14rpx;
				padding: 25rpx 15rpx;
				h2{
					margin-left: 40rpx;
					margin-bottom: 15rpx;
					font-size: 12pt;
					font-weight: normal;
				}
				ul {
					display: flex;
					background-color: #FFFFFF;
					margin: 0 auto;
					justify-content: flex-start;
					padding: 30rpx;
					border-radius: 14rpx;
					flex-wrap: wrap;
					li {
						list-style: none;
						/* 文字，图片居中 */
						text-align: center;
						width: 25%;
						margin-bottom: 40rpx;
						// margin: 10rpx 20rpx;
						a {
							text-decoration: none;
							color: #505050;
							font-weight: bold;
							image {
								width: 46rpx;
								height: 46rpx;
							}

							p {
								margin-top: 20rpx;
								font-size: 22rpx;
							}
						}
					}
				}
			}
		}

		// 我的服务
		view {
			&.serve {
				margin: 20rpx 30rpx;
				background-color: #FFFFFF;
				border-radius: 14rpx;
				padding: 25rpx 15rpx;
				h2{
					margin-left: 40rpx;
					margin-bottom: 15rpx;
					font-size: 12pt;
					font-weight: normal;
				}
				ul {
					/* ul 默认边距 */
					/* padding-left: 0; */
					display: flex;
					background-color: #FFFFFF;
					margin: 0 auto;
					// flex-direction: row;
					/* padding-top: 12rpx; */
					padding: 30rpx;
					border-radius: 14rpx;
					li {
						margin-right: 72rpx;
						list-style: none;
						/* 文字，图片居中 */
						text-align: center;

						a {
							text-decoration: none;
							color: #505050;
							font-weight: bold;

							image {
								width: 46rpx;
								height: 46rpx;
							}

							p {
								margin-top: 20rpx;
								font-size: 22rpx;
							}
						}
					}
				}

			}
		}
	}
</style>
