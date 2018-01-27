<template>
	<div id="app">
	<v_header :seller="seller"></v_header>
	<div class="tab">
		<div class="tab-item">
			<router-link to="/goods">商品</router-link>
		</div>
		<div class="tab-item">
			<router-link to="/ratings">评价</router-link>
		</div>
		<div class="tab-item">
			<router-link to="/seller">商家</router-link>
		</div>
	</div>
		<router-view/>
	</div>
</template>

<script>
	import v_header from './components/v_header/v_header'
	export default {
		name: 'App',
		components:{v_header},
		data(){
		    return {
		        seller: {},
		    }
		},
		created() {
//			var that=this;
			var url1 = 'http://localhost:3000/seller'
			this.$axios(url1)
				.then((response)=> {
					//console.log(that.seller)
					if(response.data.errno === 0) {
						this.seller = response.data.data
					}
				})
				.catch(function(error) {
					//console.log(error);
				});

		}
	}
</script>

<style>
	*{margin: 0;}
	a{text-decoration: none;}
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
	.tab{display: flex;background: white;height: 40px;border-bottom: 1px solid rgba(7,17,27,.1);}
	.tab-item{flex: 1;text-align: center;font-size: 14px;height: 40px;;}
	.tab-item a{display: block;color: rgb(77,85,93);height: 40px;line-height: 40px;}
	.tab-item .router-link-active{color: rgb(240,20,20);}
</style>