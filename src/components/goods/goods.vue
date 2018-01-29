<template>
	<div class="goods">
		<div class="menu-wrapper" ref="mwrapper">
			<ul>
				<li v-for="(item,index) in goods" class="menu-item">
					<span class="text2">
						<span class="icon2" :class="classMap[item.type]"></span>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper" ref="fwrapper">
			<ul>
				<li v-for="item in goods" class="food-list food-list-hook">
					<h1 class="titel2">{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item">
							<div class="icon3"><img :src="food.icon" alt="" width="57" height="57"/></div>
							<div class="content">
								<h2 class="name3">{{food.name}}</h2>
								<p class="desc" v-show="food.description">{{food.description}}</p>
								<div class="extra">
									<span class="extra-1">月售{{food.sellerCount}}份</span><span>好评率{{food.rating}}%</span>
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
	</div>
</template>

<script>
	import BScroll from 'better-scroll'
	export default{
		data(){
		    return {
		        goods: [],
		        classMap:[],
		        listHeight:[]
		    }
		},
		props:{
			seller:{
				Type:Object
			}
		},
		created(){
			this.classMap = ['t0','t1','t2','t3','t4']
			var url2 = 'http://localhost:3000/goods'
			this.$axios(url2)
			.then((response)=> {
				if(response.data.errno === 0) {
					this.goods = response.data.data;
				}
			})
			.catch(function(error) {
				//console.log(error);
			});
			
		},
		mounted() {
	      this.$nextTick(() => {
	        this.menuScroll = new BScroll(this.$refs.mwrapper, {});
			this.foodsScroll = new BScroll(this.$refs.fwrapper, {});
	      })
	    }
	}
</script>

<style>
	.goods{position: absolute;width: 100%;top: 180px;bottom: 46px;display: flex;overflow: hidden;}
	.menu-wrapper{flex: 0 0 80px;width: 80px;background: #f3f5f7;}
	.foods-wrapper{flex: 1;}
	ul{padding: 0;}
	li{list-style: none;}
	.menu-item{list-style: none;display: table;height: 54px;width: 56px;line-height: 14px;font-size: 0;margin: 0 auto;}
	.icon2{vertical-align: top;}
	.text2{font-size: 12px;display: table-cell;vertical-align: middle;width: 56px;text-align: center;border-bottom: 1px solid rgba(7,17,27,.1);color: rgb(77,85,93);}
	.foods-wrapper{}
	.menu-wrapper{}
	.food-list h1{height: 26px;line-height: 26px;font-size: 12px;color: rgb(147,153,159);background: #f3f5f7;text-indent: 14px;border-left:2px solid #d9dde1 ;}
	.food-item{display: flex;margin: 18px;border-bottom: 1px solid rgba(7,17,27,.1);padding-bottom: 18px;}
	.food-item:last-child{border: none;padding-bottom: 0;}
	.icon3{flex: 0 0 57px;margin-right: 10px;height: 57px;}
	.content{flex: 1;}
	.name3{font-size: 10px;margin: 2px 0 8px 0;height: 14px;line-height: 14px;color: rgb(7,17,27);}
	.desc{line-height: 16px;font-size: 10px;color: rgb(147,153,159);margin-bottom: 8px;}
	.extra{line-height: 10px;font-size: 10px;color: rgb(147,153,159);}
	.extra-1{margin-right: 12px;}
	.price{font: 0;}
	.newPrice{font-size: 10px;line-height: 24px;color: rgb(240,20,20);display: inline-block;}
	.oldPrice{font-size: 10px;line-height: 24px;color: rgb(147,153,159);display: inline-block;text-decoration: line-through;margin-left: 8px;}
	.newPrice span{font-size: 14px;font-weight: 700;}
	.oldPrice span{font-size: 14px;font-weight: 700;}
</style>