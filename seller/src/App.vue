<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px-b">
      <div class="tab-item"><router-link :to="{path: '/goods'}">商品</router-link></div>
      <div class="tab-item"><router-link :to="{path: '/ratings'}">评论</router-link></div>
      <div class="tab-item"><router-link :to="{path: '/seller'}">商家</router-link></div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import header from '@/components/header/header';
  const ERR_OK = 0;

  export default {
    data() {
      return {
        seller: {}
      };
    },
    created() {
      this.$http.get('/api/seller').then((response) => {
        response = response.body;
        if (response.error === ERR_OK) {
          this.seller = response.data;
        }
      });
    },
    components: {
      'v-header': header
    }
  };
</script>

<style>
  .tab{
    display: flex;
    height: 40px;
    line-height: 40px;
  }
  .tab-item{
    flex: 1;
    text-align: center;
  }
  .tab-item a{
    display: block;
    color: rgb(77, 85, 93);
    font-size: 14px;
  }
</style>
