<template>
	<div class="goods">
		<div class="menu-wrapper">
			<ul>
				<li v-for="(item,index) in goods" class="menu-item">
					<span class="text2">
						<span class="icon2" :class="classMap[item.type]"></span>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper">
			<ul>
				<li v-for="item in goods" class="food-list">
					<h1 class="titel2">{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item">
							<div class="icon3"><img :src="food.icon" alt="" /></div>
							<div class="content">
								<h2 class="name3">{{food.name}}</h2>
								<p class="desc" v-show="food.description">{{food.description}}</p>
								<div class="extra">
									<span>月售{{food.sellerCount}}份</span>
									<span>好评率{{food.rating}}%</span>
								</div>
								<div class="price">
									<span>￥{{food.price}}</span>
									<span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
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
	export default{
		data(){
		    return {
		        goods: [],
		        classMap:[]
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
					this.goods = response.data.data
				}
			})
			.catch(function(error) {
				//console.log(error);
			});
			
		}
	}
</script>

<style>
	.goods{position: absolute;width: 100%;top: 180px;bottom: 46px;display: flex;overflow: hidden;}
	.menu-wrapper{flex: 0 0 80px;width: 80px;background: #f3f5f7;}
	.foods-wrapper{flex: 1;}
	ul{padding: 0;}
	.menu-item{list-style: none;display: table;height: 54px;width: 56px;line-height: 14px;font-size: 0;margin: 0 auto;}
	.icon2{vertical-align: top;}
	.text2{font-size: 12px;display: table-cell;vertical-align: middle;width: 56px;text-align: center;border-bottom: 1px solid rgba(7,17,27,.1);color: rgb(77,85,93);}
	.foods-wrapper{overflow-y: auto;}
	.menu-wrapper{overflow-y: auto;}
</style>