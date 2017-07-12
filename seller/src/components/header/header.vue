<template>
  <div class="header">
  	<div class="content-wrap" @click="showDetail">
  		<div class="avatar">
  			<img width="64" height="64" :src="seller.avatar" alt="">
  		</div>
  		<div class="content">
  			<div class="title">
  				<span class="brand"></span>
  				<span class="name">{{seller.name}}</span>
  			</div>
  			<div class="description">
  				{{seller.description}}/{{seller.deliveryTime}}分钟送达
  			</div>
  			<div v-if="seller.supports" class="support">
  				<span class="icon" :class="classMap[seller.supports[0].type]"></span>
  				<span class="text">{{seller.supports[0].description}}</span>
  			</div>
  		</div>
  		<div v-if="seller.supports" class="detail">
  			{{seller.supports.length}}个<i class="icon-keyboard_arrow_right"></i>
  		</div>
  	</div>
  	<div class="bulletin-wrap">
  		<span class="bulletin-icon"></span><span class="bulletin-text">{{seller.bulletin}}</span><i class="icon-keyboard_arrow_right"></i>
  	</div>
  	<div class="background">
  		<img :src="seller.avatar" width="100%" height="100%" alt="">
  	</div>
    <transition name="fade">
      <div v-show="detailShow" class="detail-con">
        <div class="detail-wrap clearfix">
          <div class="detail-main">
            <h1 class="detail-name">{{seller.name}}</h1>
            <div class="star-wrap"><star :size="48" :score="seller.score"></star></div>
            <div class="detail-title">
              <span class="detail-title-line"></span><span class="detail-title-txt">优惠信息</span><span class="detail-title-line"></span>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item, index) in seller.supports">
                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                <span class="text">{{seller.supports[index].description}}</span>
              </li>
            </ul>
            <div class="detail-title">
              <span class="detail-title-line"></span><span class="detail-title-txt">商家广告</span><span class="detail-title-line"></span>
            </div>
            <p class="detail-bulletin">{{seller.bulletin}}</p>
          </div>
        </div>
        <div class="detail-close" @click="hiddenDetail"><i class="icon-close"></i></div>
      </div>
    </transition>
  </div>
</template>

<script>
  import star from '@/components/star/star';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hiddenDetail() {
        this.detailShow = false;
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      star
    }
  };
</script>

<style>
  @import "../../common/css/icon.css";

  .header{
  	color: #fff;
  	position: relative;
  	background: rgba(7, 17, 27, .5);
  	overflow: hidden;
  }
  .content-wrap{
  	padding: 24px 12px 18px 24px;
  	display: flex;
  	position: relative;
  }
  .avatar{
  	width: 64px;
  	height: 64px;
  	flex: 0 0 64px;
  	margin-right: 16px;
  }
  .avatar img{
  	border-radius: 2px;
  }
  .title{
  	margin: 2px 0 8px 0;
  	font-size: 0;
  }
  .brand{
  	display: inline-block;
  	width: 30px;
  	height: 18px;
  	background-image: url(./img/brand@2x.png);
    background-size: 30px 18px;
    background-repeat: no-repeat; 
  	vertical-align: middle;
  }
  .name{
  	display: inline-block;
  	vertical-align: middle;
  	margin-left: 6px;
  	font-size: 16px;
  	font-weight: bold;
  }
  .description{
  	font-size: 12px;
  	margin-bottom: 10px;
  }
  .support{
  	font-size: 0;
  }
  .text{
  	display: inline-block;
	  vertical-align: middle;
  	font-size: 10px;
	  line-height: 12px;
  }
  .support .icon{
  	display: inline-block;
  	width: 12px;
  	height: 12px;
  	vertical-align: middle;
  	margin-right: 4px;
  }
  .support .icon.decrease{
  	background: url(./img/decrease_1@2x.png) no-repeat; 
  	background-size: cover;
  }
  .support .icon.discount{
  	background: url(./img/discount_1@2x.png) no-repeat; 
  	background-size: cover;
  }
  .support .icon.guarantee{
  	background: url(./img/guarantee_1@2x.png) no-repeat; 
  	background-size: cover;
  }
  .support .icon.invoice{
  	background: url(./img/invoice_1@2x.png) no-repeat; 
  	background-size: cover;
  }
  .support .icon.special{
  	background: url(./img/special_1@2x.png) no-repeat; 
  	background-size: cover;
  }
  .support-item{
    margin-bottom: 12px;
    font-size: 0;
  }
  .support-item .icon{
    display: inline-block;
    vertical-align: middle;
    width: 16px;
    height: 16px;
    margin-right: 6px;
    background-repeat: no-repeat;
    background-size: cover;
  }
  .support-item .icon.decrease{
    background-image: url(./img/decrease_2@2x.png);  
  }
  .support-item .icon.discount{
    background-image: url(./img/discount_2@2x.png); 
  }
  .support-item .icon.guarantee{
    background-image: url(./img/guarantee_2@2x.png); 
  }
  .support-item .icon.invoice{
    background-image: url(./img/invoice_2@2x.png); 
  }
  .support-item .icon.special{
    background-image: url(./img/special_2@2x.png); 
  }
  .detail{
  	position: absolute;
  	right: 12px;
  	bottom: 14px;
  	border-radius: 14px;
  	display: inline-block;
  	text-align: center;
  	background: rgba(0, 0, 0, .2);
  	font-size: 10px;
  	height: 24px;
  	line-height: 24px;
  	padding: 0px 8px;
  }
  .bulletin-wrap{
  	padding: 0 12px;
  	height: 28px;
  	background: rgba(7, 17, 27, .2);
  	position: relative;
  }
  .bulletin-wrap .icon-keyboard_arrow_right{
  	position: absolute;
  	right: 12px;
  	top: 10px;
  	font-size: 10px;
  }
  .bulletin-icon{
  	display: block;
  	float: left;
  	width: 22px;
  	height: 12px;
  	background-image: url(./img/bulletin@2x.png);
  	background-size: 22px 12px; 
    background-repeat: no-repeat;
  	margin-top: 8px;
  	margin-right: 4px;
  }
  .bulletin-text{
  	display: block;
  	font-size: 10px;
  	margin-right: 12px;
  	height: 28px;
  	line-height: 28px;
  	white-space: nowrap;
  	overflow: hidden;
  	text-overflow: ellipsis;
  }
  .background{
  	position: absolute;
  	top: 0;
  	bottom: 0;
  	left: 0;
  	right: 0;
  	z-index: -1;
  	filter: blur(10px);
  }
  .detail-con{
    position: fixed;
    overflow: auto;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    height: 100%;
    z-index: 9;
    background: rgba(7,17,27,.8);
  }
  .fade-enter-active, .fade-leave-active{
    transition: opacity .5s
  }
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }
  .detail-wrap{
    min-height: 100%;
    width: 100%;
  }
  .detail-wrap .supports{
    padding: 0 12px;
  }
  .detail-main{
    margin-top: 64px;
    padding-bottom: 64px;
    padding-left: 36px;
    padding-right: 36px;
  }
  .detail-close{
    position: relative;
    width: 32px;
    height: 32px;
    margin: -64px auto 0 auto;
    clear: both;
    font-size: 32px;
  }
  .detail-close i{
    color: rgba(255,255,255,.5);
  }
  .detail-name{
    font-size: 16px;
    text-align: center;
    font-weight: 700;
  }
  .star-wrap{
    margin: 16px 0 28px;
    padding: 2px 0;
    text-align: center;
  }
  .detail-title{
    text-align: center;
    display: flex;
    align-items: center;
    margin: 28px 0 24px;
  }
  .detail-title .detail-title-line{
    flex: 1;
  }
  .detail-title-txt{
    padding: 0 12px;
    font-size: 14px;
  }
  .detail-title-line{
    height: 1px;
    background: rgba(255,255,255,.2);
  }
  .detail-bulletin{
    padding: 0 12px;
    font-size: 12px;
    line-height: 2;
  }
  @media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
  	.brand{
  	  background-image: url(./img/brand@3x.png);
  	}
    .bulletin-icon{
      background-image: url(./img/bulletin@3x.png);
    }
  	.support .icon.decrease{
  	  background-image: url(./img/decrease_1@3x.png); 
  	}
  	.support .icon.discount{
  	  background-image: url(./img/discount_1@3x.png); 
  	}
  	.support .icon.guarantee{
  	  background-image: url(./img/guarantee_1@3x.png); 
  	}
  	.support .icon.invoice{
  	  background-image: url(./img/invoice_1@3x.png); 
  	}
  	.support .icon.special{
  	  background-image: url(./img/special_1@3x.png); 
  	}
  	.bulletin{
  	  background-image: url(./img/bulletin@3x.png) 
  	}
    .support-item .icon.decrease{
      background-image: url(./img/decrease_2@3x.png);
    }
    .support-item .icon.discount{
      background-image: url(./img/discount_2@3x.png);
    }
    .support-item .icon.guarantee{
      background-image: url(./img/guarantee_2@3x.png);
    }
    .support-item .icon.invoice{
      background-image: url(./img/invoice_2@3x.png);
    }
    .support-item .icon.special{
      background-image: url(./img/special_2@3x.png);
    }
  }
</style>
