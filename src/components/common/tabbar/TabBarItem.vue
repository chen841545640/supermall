<template>
 <div class="tab-bar-item" @click="itemClick">
   <!-- 使用插槽时，建议在外包裹一层div -->
   <div v-if="!isActive"><slot name="item-icon"></slot></div>
   <div v-else><slot name="item-icon-active"></slot></div>
   <div :style="activeStyle"><slot name="item-text"></slot></div>
 </div>
</template>
<script>
export default {
  name:'TabBarItem',
  props:{
    //动态获取路径
    path:String,
    activeColor:{
      type:String,
      default:'red'//默认颜色
    }
  },
 computed: {
   isActive(){
     //indexOf方法：如果从所给中找到了所需要的则为-1既true
     ///home ->item1(/home) =true
     ///home ->item1(/category) =flase
     return this.$route.path.indexOf(this.path) !==-1
   },
   activeStyle(){
     return this.isActive ? {color:this.activeColor} : {}
   }
 },
  methods: {
    itemClick(){
      this.$router.push(this.path)
    }
  },
}
</script>
<style>
  .tab-bar-item{
  flex: 1;
  text-align: center;
  /* 开发中一般tabbar的高度为49px */
  height: 49px;
  font-size: 14px;
}
.tab-bar-item img{
  height: 24px;
  width: 24px;
  margin-top: 3px;
  vertical-align: middle;
  margin-bottom: 2px;
}

</style>