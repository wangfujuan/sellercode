<template>
  <div class="goods">
  	<div class="menu-wrap" ref="menuWrapper">
  	  <ul class="menu-list" v-for="good in goods">
  	  	<li class="menu-item border-1px-b">
  		  	<span class="text"><span class="icon" v-show="good.type>0" :class="classMap[good.type]"></span>{{good.name}}</span>
  	  	</li>
  	  </ul>
  	</div>
  	<div class="foods-wrap" ref="foodsWrapper">
  		<div class="food-cate-item" v-for="item in goods">
  			<h2 class="foods-title">{{item.name}}</h2>
  			<ul class="foods" v-for="food in item.foods">
  				<li class="food-item border-1px-b">
  					<div class="food-pic"><img width="57" height="57" :src="food.image" alt=""></div>
  					<div class="food-info">
  						<div class="food-name">{{food.name}}</div>
  						<div class="food-description">{{food.description}}</div>
  						<div class="food-sell"><span>月销{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span></div>
  						<div class="food-price"><span class="newprice"><i>¥</i>{{food.price}}</span><span class="oldprice" v-show="food.oldPrice">¥{{food.oldPrice}}</span></div>
  					</div>
  				</li>
  			</ul>
  		</div>
  	</div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll';
  const ERR_OK = 0;

  export default {
    data() {
      return {
        goods: {}
      };
    },
    created() {
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        // console.log(response);
        if (response.error === ERR_OK) {
          this.goods = response.data;
          this._initScroll();
        }
      });
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    methods: {
      _initScroll() {
        console.log(this.$refs.menuWrapper);
        console.log(this.$refs.foodsWrapper);
        this.meunScroll = new BScroll(this.$refs.menuWrapper, {});
        this.foodScroll = new BScroll(this.$refs.foodsWrapper, {});
      }
    }
  };
</script>

<style>
  .goods{
  	display: flex;
  	position: absolute;
  	top: 174px;
  	bottom: 46px;
  	width: 100%;
  	overflow: hidden;
  }
  .menu-wrap{
		flex: 0 0 80px;
		width: 80px;
		background: #f3f5f7;
  }
  .foods-wrap{
  	flex: 1;
  }
  .menu-list{
  	padding: 0 12px;
  }
  .menu-item{
  	display: table;
  	height: 54px;
  	width: 56px;
  	color: #07111b;
  	line-height: 14px;
  }
  .menu-item .text{
  	display: table-cell;
  	width: 56px;
  	vertical-align: middle;
  	font-size: 12px;
  }
  .menu-item .icon{
  	display: inline-block;
    width: 12px;
    height: 12px;
    margin-right: 2px;
    background-repeat: no-repeat;
    background-size: 12px 12px;
    vertical-align: top;
  }
  .menu-item .icon.decrease{
    background-image: url(./img/decrease_3@2x.png);  
  }
  .menu-item .icon.discount{
    background-image: url(./img/discount_3@2x.png); 
  }
  .menu-item .icon.guarantee{
    background-image: url(./img/guarantee_3@2x.png); 
  }
  .menu-item .icon.invoice{
    background-image: url(./img/invoice_3@2x.png); 
  }
  .menu-item .icon.special{
    background-image: url(./img/special_3@2x.png); 
  }
  .foods-title{
  	background: #f3f5f7;
  	font-size: 12px;
  	border-left: 2px solid #d9dde1;
  	padding: 0 14px;
  	color: rgb(147, 153, 159);
  	line-height: 26px;
  }
  .food-item{
  	display: flex;
		padding: 18px;
  }
  .food-pic{
		flex: 0 0 57px;
		width: 57px;
  }
  .food-info{
		flex: 1;
		margin-left: 10px;
  }
  .food-name{
  	font-size: 14px;
  	color: rgb(7,17,27);
  	margin-top: 2px;
  }
  .food-description{
  	color: rgb(147, 153, 159);
  	font-size: 10px;
  	margin: 8px 0;
  }
  .food-sell{
  	margin: 8px 0;
  	font-size: 0;
  }
  .food-sell span{
		color: rgb(147, 153, 159);
  	font-size: 10px;
  	margin-right: 12px;
  	display: inline-block;
  }
  .newprice{
  	font-size: 14px;
  	font-weight: 700;
  	color: #f01414;
  	margin-right: 8px;
  }
  .newprice i{
  	font-style: normal;
  	font-size: 10px;
  }
  .food-price{
  	font-size: 0;
  }
  .oldprice{
  	font-size: 10px;
  	color: rgb(147, 153, 159);
  	text-decoration: line-through;
  }
  @media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
  	.menu-item .icon.decrease{
	    background-image: url(./img/decrease_3@3x.png);  
	  }
	  .menu-item .icon.discount{
	    background-image: url(./img/discount_3@3x.png); 
	  }
	  .menu-item .icon.guarantee{
	    background-image: url(./img/guarantee_3@3x.png); 
	  }
	  .menu-item .icon.invoice{
	    background-image: url(./img/invoice_3@3x.png); 
	  }
	  .menu-item .icon.special{
	    background-image: url(./img/special_3@3x.png); 
	  }
  }
</style>
