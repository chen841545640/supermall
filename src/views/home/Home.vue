<template>
  <div id="home">
    <nav-bar class="home-bar">
      <template v-slot:center>
      <div>购物街</div>
      </template>
      </nav-bar>
      <home-swiper :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control class="tab-control" :titles="['流行','新款','精选']" @tabClick="tabClick"></tab-control>
      <goods-list :goods="showGoods"></goods-list>
    <!-- <ul>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
      <li>数据</li>
    </ul> -->
      <back-top></back-top>
  </div>
</template>
<script>
import NavBar from "../../components/common/navbar/NavBar"
import TabControl from "../../components/content/tabControl/TabControl"
import GoodsList from "../../components/content/goods/GoodsList"

import HomeSwiper from "./childComps/HomeSwiper"
import RecommendView from "./childComps/RecommendView"
import FeatureView from "./childComps/FeatureView"

import {getHomeMultidata,getHomeGoods } from "../../network/home"
import BackTop from '../../components/content/backTop/BackTop.vue'



export default {
  name:'Home',
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },
  data() {
    return {
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      },
      currentType:'pop'
    }
  },
  components:{
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    BackTop
  
  },
  created() {
    //1.请求多个数据
   this.getHomeMultidata()
    //请求商品数据
    this.getHomeGoods('pop')
     this.getHomeGoods('new')
      this.getHomeGoods('sell')
  },
  methods: {
     /**
     * 事件监听相关方法
     */
    tabClick(index){
      switch(index){
        case 0:
          this.currentType='pop'
          break          
           case 1:
          this.currentType='new'
          break
           case 2:
          this.currentType='sell'        
      }
    },
    /**
     * 网络请求相关方法
     */
    getHomeMultidata(){
      //1.请求多个数据
    getHomeMultidata().then(res => {
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend.list;
    })
    },
    getHomeGoods(type){
       2//请求商品数据
       const page=this.goods[type].page + 1
    getHomeGoods(type,page).then(res =>{
      //push(...)会对函数进行解析，然后依次将数据依次填入到数组中
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
    })
    }
  },
}
</script>
<style>
#home{

   height: 100vh;
    position: relative;
}
  .home-bar{
    background-color:var(--color-tint);
    color:#fff;
    position:fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }
.tab-control{
  position: sticky;
  top: 44px;
  z-index: 9;
}
</style>