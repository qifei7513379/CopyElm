<template>
	<div class="goods">
		<div class="menu-wrapper" ref="mwrapper">
			<ul>
				<li v-for="(item,index) in goods" class="menu-item" :class="{'current': currentIndex === index}" @click="selectMenu(index, $event)">
					<span class="text">
						<span class="icon" :class="classMap[item.type]"></span>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper" ref="fwrapper">
			<ul>
				<li v-for="item in goods" class="food-list food-list-hook" ref="foodlisthook">
					<h1>{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item">
							<div class="icon"><img :src="food.icon" alt="" width="57" height="57"/></div>
							<div class="content">
								<h2 class="name">{{food.name}}</h2>
								<p class="desc" v-show="food.description">{{food.description}}</p>
								<div class="extra">
									<span class="perm">月售{{food.sellerCount}}份</span><span>好评率{{food.rating}}%</span>
								</div>
								<div class="price">
									<span class="newPrice">￥<span>{{food.price}}</span></span><span v-show="food.oldPrice" class="oldPrice">￥<span>{{food.oldPrice}}</span></span>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
		<shopcart></shopcart>
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	import shopcart from '@/components/shopcart/shopcart'
	export default{
		data(){
		    return {
		        goods: [],
		        classMap:[],
		        listHeight:[],
		        scrollY:0
		    }
		},
		props:{
			seller:{
				Type:Object
			}
		},
		computed: {
            currentIndex() {
                for (let i = 0; i < this.listHeight.length; i++) {
                    let height1 = this.listHeight[i];
                    let height2 = this.listHeight[i + 1];
                    if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
                        return i;
                    }
                }
                return 0;
            }
       },
		created(){
			this.classMap = ['t0','t1','t2','t3','t4']
			var url2 = 'http://localhost:3000/goods'
			this.$axios(url2)
			.then((response)=> {
				if(response.data.errno === 0) {
					this.goods = response.data.data;
					this.$nextTick(() => {
				        this._initScroll();
				        this._calculateHeight()
				      })
				}
			})
			.catch(function(error) {
				//console.log(error);
			});
			
		},
		methods: {
			_initScroll() {
		      	this.menuScroll = new BScroll(this.$refs.mwrapper, {
		      		click: true
		      	});
				this.foodsScroll = new BScroll(this.$refs.fwrapper, {
					click: true,
                    probeType: 3 // 监测实时滚动的位置
				});
				this.foodsScroll.on('scroll', (pos) => {
                    // 拿到实时的y坐标
                    this.scrollY = Math.abs(Math.round(pos.y));
                })
				
			},
			_calculateHeight() {
                // 获取食物的li Dom节点列表
                let foodList = this.$refs.foodlisthook;               
                let height = 0;
                this.listHeight.push(height);
                for (let i = 0; i < foodList.length; i++) {
                    let item = foodList[i];
                    height += item.clientHeight;
                    this.listHeight.push(height);                  
                }
            },
            selectMenu(index, event) {
                // better-scroll 可以监听到此事件，浏览器原生不能监听到  防止pc端出现两次点击
                if (!event._constructed) {
                    return;
                }
                // 获取食物的li Dom节点列表
                let foodList = this.$refs.foodlisthook;
                let el = foodList[index];
                // 调用better-scroll 方法滚动到响应位置
                this.foodsScroll.scrollToElement(el, 300);
            }
	   },
	   components:{
	   	shopcart
	   }
	}
</script>

<style lang="scss" scoped="" type="text/css">
	.goods {
		position: absolute;
		width: 100%;
		top: 180px;
		bottom: 46px;
		display: flex;
		overflow: hidden;		
		.menu-wrapper {
			flex: 0 0 80px;
			width: 80px;
			background: #f3f5f7;			
			.menu-item {
				list-style: none;
				display: table;
				height: 54px;
				width: 56px;
				line-height: 14px;
				font-size: 0;
				padding: 0 12px;				
				.text {
					font-size: 12px;
					display: table-cell;
					vertical-align: middle;
					width: 56px;
					text-align: center;
					border-bottom: 1px solid rgba(7,17,27,.1);
					color: rgb(77,85,93);
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
			.current {
				position: relative;
				margin-top: -1px;
				z-index: 10;
				background: #fff;
				font-weight: 700;
				.text {
					border: none;
				}
			}
	
		}
		.foods-wrapper {
			flex: 1;
			.food-list {
				h1 {
					height: 26px;
					line-height: 26px;
					font-size: 12px;
					color: rgb(147,153,159);
					background: #f3f5f7;
					text-indent: 14px;
					border-left:2px solid #d9dde1 ;
				}
				ul{
					.food-item {
						display: flex;
						margin: 18px;
						border-bottom: 1px solid rgba(7,17,27,.1);
						padding-bottom: 18px;
						.icon {
							flex: 0 0 57px;
							margin-right: 10px;
							height: 57px;
						}
						&:last-child {
							border: none;
							padding-bottom: 0;
						}
						.content {
							flex: 1;							
							.name {
								font-size: 10px;
								margin: 2px 0 8px 0;
								height: 14px;
								line-height: 14px;
								color: rgb(7,17,27);
							}
							.desc {
								line-height: 16px;
								font-size: 10px;
								color: rgb(147,153,159);
								margin-bottom: 8px;
							}
							.extra {
								line-height: 10px;
								font-size: 10px;
								color: rgb(147,153,159);
								.perm {
									margin-right: 12px;
								}
							}
							.price {
								font-size: 0;
								.newPrice {
									font-size: 10px;
									line-height: 24px;
									color: rgb(240,20,20);
									display: inline-block;
								}
								.oldPrice{
									font-size: 10px;
									line-height: 24px;
									color: rgb(147,153,159);
									display: inline-block;
									text-decoration: line-through;
									margin-left: 8px;
								}
								.newPrice,.oldPrice {
									span {
										font-size: 14px;font-weight: 700;
									}
								}
							}
						}
					}
				}
			}
		}
	}
</style>