<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrapper">
					<div class="logo">
						<i class="icon-shopping_cart"></i>
					</div>
				</div>
				<div class="price">
					￥{{totalPrice}}元
				</div>
				<div class="desc">
					另需配送费{{deliveryprice}}元
				</div>
			</div>
			<div class="content-right">
				<div class="pay">￥{{minprice}}元起送</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		props:{
			deliveryprice:{
				type:Number
			},
			minprice:{
				type:Number
			},
			selectfoods:{
				type:Array,
				default(){
					return [];
				}
			}
		},
		computed:{
			totalPrice(){
				let total = 0;
				this.selectfoods.forEach((food)=>{
					total += food.price*food.count;
				})
				return total;
			},
			totalCount(){
				let count = 0;
				this.selectfoods.forEach((food)=>{
					count += food.count;
				})
				return count;
			}
		}
	}
</script>

<style lang="scss" scoped="" type="text/css">
	.shopcart{
		position: fixed;
		left: 0;
		bottom: 0;
		z-index: 50;
		width: 100%;
		height: 48px;
		.content{
			display: flex;
			background: #141d27;
			font-size: 0;
			.content-left{
				flex: 1;				
				.logo-wrapper{
					display: inline-block;
					position: relative;
					top: -10px;
					margin: 0 12px;
					padding: 6px;
					width: 56px;
					height: 56px;
					box-sizing: border-box;
					vertical-align: top;
					border-radius: 50%;
					background: #141d27;
					.logo{
						width: 100%;
						height: 100%;
						border-radius: 50%;
						background: #2b343c;
						text-align: center;
						.icon-shopping_cart {
							font-size: 24px;
							color: #80858a;
							line-height: 44px;							
						}
					}
				}
				.price{
					display: inline-block;
					vertical-align: top;
					line-height: 24px;
					margin-top: 12px;
					box-sizing: border-box;
					padding-right: 12px;
					border-right: 1px solid rgba(255,255,255,.1);
					font-size: 16px;
					font-weight: 700;
					color: rgba(255,255,255,.4);
				}
				.desc{
					display: inline-block;
					vertical-align: top;
					line-height: 24px;
					margin: 12px 0 0 12px;
					font-size: 10px;
					color: rgba(255,255,255,.4);
				}	
			}
			.content-right{
				flex: 0 0 105px;
				width: 105px;
				.pay{
					line-height: 48px;
					height: 48px;
					text-align: center;
					font-size: 12px;
					color: rgba(255,255,255,.4);
					font-weight: 700;
					background: #2b333b;
				}
			}
		}
	}
</style>