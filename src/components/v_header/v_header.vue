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
						<span class="icon" :class="classMap[seller.supports[0].type]"></span>										
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
				<div class="tanceng-wrapper clearfix">
					<div class="tanceng-main">
						<h1 class="name">{{seller.name}}</h1>
						<div class="star-wraper">
							<star :size="48" :score="seller.score"></star>
						</div>
						<div class="minTitle">
							<div class="line"></div>
							<div class="text">优惠信息</div>
							<div class="line"></div>
						</div>
						<ul v-if="seller.supports" class="supports">
							<li class="support-item" v-for="(item,index) in seller.supports">
								<span class="icon" :class="classMap[seller.supports[index].type]"></span>
								<span class="text">{{seller.supports[index].description}}</span>
							</li>
						</ul>						
						<div class="minTitle">
							<div class="line"></div>
							<div class="text">商家公告</div>
							<div class="line"></div>
						</div>
						<div class="bulletin">
							{{seller.bulletin}}
						</div>						
					</div>
				</div>
				<div class="close" @click="close">
					×
				</div>
			</div>
		</transition>
	</div>	
	
</template>

<script>
	import star from '../star/star'
	export default{
		name:'v_header',
		components:{star},
		data(){
			return{
				show:false,
				classMap:[]
			}
		},
		created(){
			this.classMap = ['t0','t1','t2','t3','t4']
		},
		props: ['seller'],
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

<style lang="scss" scoped="" type="text/css">
	.v_header{
		position: relative;
		background: rgba(7,17,27,.5);
		.up-head{
			overflow: hidden;
			position: relative;
			.head{
				padding: 24px 0 18px 24px;
				font-size: 0;
				position: relative;
				.avatar{
					display: inline-block;
					border-radius: 2px;
				}
				.head-info{
					display: inline-block;
					vertical-align: top;
					margin-left: 16px;
					.title{
						font-size: 16px;
						color: white;
						font-weight: bold;
						line-height: 18px;
						margin-top: 2px;
						span{
							background: url(brand@2x.png) no-repeat;
							display: inline-block;
							width: 32px;
							height: 18px;
							background-size: 100% 100%;
							vertical-align: top;
						}
						div{
							line-height: 18px;
							display: inline-block;
							margin-left: 6px;
						}
					}
					.type{
						font-size: 12px;
						line-height: 12px;
						color: white;
						font-weight: 200;
						margin-top: 8px;
					}
					.active{
						font-size: 10px;
						line-height: 12px;
						color: white;
						font-weight: 200;
						margin-top: 10px;						
					    .t0 {
							background: url(decrease_1@2x.png) no-repeat;
							width: 12px;
							height: 12px;
							background-size: 100% 100%;
							display: inline-block;
							vertical-align: top;
							margin-right: 4px;
						}
						.t1{
							background: url(discount_1@2x.png) no-repeat;
							width: 12px;
							height: 12px;
							background-size: 100% 100%;
							display: inline-block;
							vertical-align: top;
							margin-right: 4px;
						}
						.t2{
							background: url(guarantee_1@2x.png) no-repeat;
							width: 12px;
							height: 12px;
							background-size: 100% 100%;
							display: inline-block;
							vertical-align: top;
							margin-right: 4px;
						}
						.t3{
							background: url(invoice_1@2x.png) no-repeat;
							width: 12px;
							height: 12px;
							background-size: 100% 100%;
							display: inline-block;
							vertical-align: top;
							margin-right: 4px;
						}
						.t4{
							background: url(special_1@2x.png) no-repeat;
							width: 12px;
							height: 12px;
							background-size: 100% 100%;
							display: inline-block;
							vertical-align: top;
							margin-right: 4px;
						}						
					}
				}
				.count{
					font-size: 10px;
					color: white;
					position: absolute;
					right: 12px;
					bottom: 15px;
					padding: 7px 8px;
					background: rgba(0,0,0,.2);
					border-radius:16px;
				}
			}
			.notice{
				background: rgba(0,0,0,.2);
				color: white;
				text-overflow: ellipsis;
				overflow: hidden;
				white-space: nowrap;
				padding:8px 24px 8px 12px;
				position: relative;
				span{
					display: inline-block;
					background: url(bulletin@2x.png) no-repeat;
					width: 32px;
					height: 18px;
					background-size: 100% 100%;
					margin-right: 4px;
					vertical-align: top;
				}
				.bulletin{
					font-size: 10px;
					color: white;
					display: inline;
					line-height: 10px;
				}
				.jiantou{
					position: absolute;
					top: 8px;
					right: 12px;
				}
			}
			.bg{
				width: 100%;
				position: absolute;
				top: 0;
				z-index: -1;
				left: 0;
				filter: blur(10px);
				overflow: hidden;
				.head-bg{
					width: 100%;
				}
			}
		}
		.tanceng{
			position: fixed;
			top: 0;
			width: 100%;
			background: rgba(7,17,27,.8);
			z-index: 100;
			overflow: auto;
			height: 100%;
			padding-bottom: 64px;
			.tanceng-wrapper{
				min-height: 100%;
				width: 100%;				
				.tanceng-main{
					margin-top: 64px;
					padding-bottom: 64px;
					.name{
						font-weight: 700;
						color: white;
						font-size: 16px;
						line-height: 16px;
						text-align: center;
					}
					.star-wraper{
						margin-top: 18px;
						padding: 2px 0;
						text-align: center;
					}
					.minTitle{
						width: 80%;
						margin: 28px auto 24px auto;
						display: flex;
						.line{
							flex: 1;
							position: relative;
							top: -8px;
							border-bottom: 1px solid rgba(255,255,255,.2);
						}
						.text{
							padding: 0 12px;
							font-size: 14px;
							color: white;
							font-weight: 700;
						}	
					}
					.supports{
						width: 76%;
						margin: 0 auto;
						padding: 0;												
						.support-item {
							list-style: none;
							font-size: 0;
							margin-bottom: 12px;
							.text{
								font-size: 12px;
								font-weight: 200;
								margin-left: 6px;
								color: white;
							}
							.t0 {
								background: url(decrease_1@2x.png) no-repeat;
								width: 12px;
								height: 12px;
								background-size: 100% 100%;
								display: inline-block;
								vertical-align: top;
								margin-right: 4px;
							}
							.t1{
								background: url(discount_1@2x.png) no-repeat;
								width: 12px;
								height: 12px;
								background-size: 100% 100%;
								display: inline-block;
								vertical-align: top;
								margin-right: 4px;
							}
							.t2{
								background: url(guarantee_1@2x.png) no-repeat;
								width: 12px;
								height: 12px;
								background-size: 100% 100%;
								display: inline-block;
								vertical-align: top;
								margin-right: 4px;
							}
							.t3{
								background: url(invoice_1@2x.png) no-repeat;
								width: 12px;
								height: 12px;
								background-size: 100% 100%;
								display: inline-block;
								vertical-align: top;
								margin-right: 4px;
							}
							.t4{
								background: url(special_1@2x.png) no-repeat;
								width: 12px;
								height: 12px;
								background-size: 100% 100%;
								display: inline-block;
								vertical-align: top;
								margin-right: 4px;
							}
						}
					}
					.bulletin{
						color: white;
						margin: 0 auto;
						width: 76%;
						font-size: 12px;
						font-weight: 200;
						line-height: 24px;
						text-align: justify;
					}	
				}
			}
			.close{
				font-size: 32px;
				color: white;
				position: relative;
				text-align: center;
				width: 100%;
				height: 64px;
				line-height: 32px;
				margin-top: -64px;
				clear: both;
			}
		}
		.fade-enter-active, .fade-leave-active {
		  transition: opacity .5s;
		}
		.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
		  opacity: 0;
		}		
	}
</style>