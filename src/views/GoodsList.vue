<template>
		<div>
			<nav-header></nav-header>

			<nav-bread>
				<span>Goods</span>

			</nav-bread>


			<div class="accessory-result-page accessory-page">
				<div class="container">
					<div class="filter-nav">
						<span class="sortby">Sort by:</span>
						<a href="javascript:void(0)" class="default cur">Default</a>
						<a href="javascript:void(0)" class="price">Price <svg class="icon icon-arrow-short"><use xlink:href="#icon-arrow-short"></use></svg></a>
						<a href="javascript:void(0)" class="">Filter by</a>
					</div>
					<div class="accessory-result">

						<!-- filter -->
						<div class="filter stopPop" id="filter" >
							<dl class="filter-price">
								<dt>Price:</dt>
								<dd ><a href="javascript:void(0)" :class="{'cur':priceChecked == 'all'}" @click="priceChecked='all'">All</a></dd>
								<dd v-for="(price,index) in priceFliter">
									<a href="javascript:void(0)" :class="{'cur':priceChecked == index}" @click="priceChecked=index">{{price.startPrice}} - {{price.endPrice}}</a>
								</dd>

							</dl>
						</div>

						<!-- search result accessories list -->
						<div class="accessory-list-wrap">
							<div class="accessory-list col-4">
								<!--商品页面-->
								<ul>
									<li v-for="(item,index) in GoodsList">
										<div class="pic">
											<a href="#"><img v-lazy="'/static/'+item.prodcutImg" alt=""></a>
										</div>
										<div class="main">
											<div class="name">{{item.productName}}</div>
											<div class="price">{{item.prodcutPrice}}</div>
											<div class="btn-area">
												<a href="javascript:;" class="btn btn--m">加入购物车</a>
											</div>
										</div>
									</li>

								</ul>
							</div>
						</div>
					</div>
				</div>
      </div>

			<nav-footer></nav-footer>

		</div>
</template>
<script>
		import './../assets/css/base.css'
		import './../assets/css/product.css'
		import NavHeader from './../components/NavHeader'
		import NavFooter from './../components/NavFooter'
		import NavBread from './../components/NavBread'
		import axios from 'axios'

		export default{
			data(){
				return{
					GoodsList:[],
          priceFliter:[
            {startPrice:'0',
              endPrice:'200'},
            {startPrice:'200',
              endPrice:'500'},
            {startPrice:'500',
              endPrice:'1000'},
            {startPrice:'1000',
              endPrice:'2000'},
          ],
          priceChecked:'all',

        }

			},
				components: {
					NavHeader,
					NavFooter,
					NavBread
				},
				mounted: function () {
					this.getGoodsList()
				},
				methods:{
					getGoodsList(){
						axios.get('/goods').then((result)=>{
							var res = result.data;
							this.GoodsList = res.result
						})
					},

				}
		}
</script>
