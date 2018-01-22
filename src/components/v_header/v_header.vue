<template>
	<div class="v_header">
		<div class="up-head">
			<div class="head">
				<img :src="seller.avatar" width="64" height="64" class="avatar"/>
				<div class="head-info">
					<div class="title">
						<span></span><div>{{seller.name}}</div>
					</div>
					<div class="type">
						{{seller.description}}/{{seller.deliveryTime}}分钟送达
					</div>
					<div class="active" v-if="seller.supports">										
						<span :class="change[seller.supports[0].type]"></span>										
						{{seller.supports[0].description}}
					</div>
				</div>
				<div class="count" v-if="seller.supports" @click="tanceng">
					{{seller.supports.length}}个  &nbsp;&nbsp;›
				</div>				
			</div>
			<div class="notice" @click="tanceng">
				<span></span>
				<div class="bulletin">
					{{seller.bulletin}}
				</div>
				<div class="jiantou">
					›
				</div>
			</div>
			<div class="bg">
				<img :src="seller.avatar" class="head-bg"/>
			</div>
		</div>
		
			
		<transition name="fade">
			<div v-if="show" class="tanceng">
				<div class="close" @click="close">
					×
				</div>
			</div>
		</transition>
	</div>	
	
</template>

<script>
	export default{
		name:'v_header',
		data(){
			return{
				change:[],
				show:false
			}
		},
		props: ['seller'],
		created(){
			this.change = ["t0","t1","t2","t3","t4"]
		},
		methods:{
			tanceng:function (){
				this.show = true	
			},
			close:function(){
				this.show = false
			}
		}
	}
</script>

<style>
	.v_header{position: relative;background: rgba(7,17,27,.5);}
	.bg{width: 100%;position: absolute;top: 0;z-index: -1;left: 0;filter: blur(10px);overflow: hidden;}
	.head-bg{width: 100%;}
	.head{padding: 24px 0 18px 24px;font-size: 0;position: relative;}
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
	.notice{background: rgba(0,0,0,.2);color: white;text-overflow: ellipsis;overflow: hidden;white-space: nowrap;padding:8px 24px 8px 12px;position: relative;}
	.notice span{display: inline-block;background: url(bulletin@2x.png) no-repeat;width: 32px;height: 18px;background-size: 100% 100%;margin-right: 4px;vertical-align: top;}
	.bulletin{font-size: 10px;color: white;display: inline;line-height: 10px;}
	.jiantou{position: absolute;top: 8px;right: 12px;}
	.count{font-size: 10px;color: white;position: absolute;right: 12px;bottom: 15px;padding: 7px 8px;background: rgba(0,0,0,.2);border-radius:16px;}
	.tanceng{position: absolute;top: 0;width: 100%;height: 100vh;background: rgba(7,17,27,.8);z-index: 999;}
	.fade-enter-active, .fade-leave-active {
	  transition: opacity .5s;
	}
	.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
	  opacity: 0;
	}
	.up-head{overflow: hidden;position: relative;}
	.close{font-size: 36px;color: white;}














</style>