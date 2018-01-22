<template>
	<div class="v_header">
		<div class="head">
			<img :src="seller.avatar" width="64" height="64" class="avatar"/>
			<div class="head-info">
				<div class="title">
					<span></span><div>{{seller.name}}</div>
				</div>
				<div class="type">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div class="active">
					<span :class="change[seller.supports[0].type]"></span>{{seller.supports[0].description}}
				</div>
			</div>
			
		</div>
		<div class="notice">
			
		</div>
		<div class="bg">
			<img :src="seller.avatar" class="head-bg"/>
		</div>
		
	</div>	
</template>

<script>
	export default{
		name:'v_header',
		data(){
			return{
				
			}
		},
		props: {
		    seller: {
		    	type:Object
		    }
		},
		created(){
			this.change = ["t0","t1","t2","t3","t4"]
		}
	}
</script>

<style>
	.v_header{overflow: hidden;position: relative;}
	.bg{width: 100%;position: absolute;top: 0;z-index: -1;left: 0;filter: blur(10px);overflow: hidden;}
	.head-bg{width: 100%;}
	.head{padding: 24px 0 18px 24px;background: rgba(7,17,27,.5);font-size: 0;}
	.avatar{display: inline-block;border-radius: 2px;}
	.head-info{display: inline-block;vertical-align: top;margin-left: 16px;}
	.title{font-size: 16px;color: white;font-weight: bold;line-height: 18px;margin-top: 2px;}
	.title span{background: url(brand@2x.png) no-repeat;display: inline-block;width: 32px;height: 18px;background-size: 100% 100%;vertical-align: top;}
	.title div{line-height: 18px;display: inline-block;margin-left: 6px;}
	.type{font-size: 12px;line-height: 12px;color: white;font-weight: 200;margin-top: 8px;}
	.active{font-size: 10px;line-height: 12px;color: white;font-weight: 200;margin-top: 10px;}
	.t0{background: url(decrease_1@2x.png) no-repeat;width: 12px;height: 12px;background-size: 100% 100%;display: inline-block;vertical-align: top;margin-right: 4px;}
	.t1{background: url(discount_1@2x.png) no-repeat;width: 12px;height: 12px;background-size: 100% 100%;display: inline-block;vertical-align: top;margin-right: 4px;}
	.t2{background: url(guarantee_1@2x.png) no-repeat;width: 12px;height: 12px;background-size: 100% 100%;display: inline-block;vertical-align: top;margin-right: 4px;}
	.t3{background: url(invoice_1@2x.png) no-repeat;width: 12px;height: 12px;background-size: 100% 100%;display: inline-block;vertical-align: top;margin-right: 4px;}
	.t4{background: url(special_1@2x.png) no-repeat;width: 12px;height: 12px;background-size: 100% 100%;display: inline-block;vertical-align: top;margin-right: 4px;}





















</style>