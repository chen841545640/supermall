//  每个组件里只封装所对应的内容，如tabbar只封装tabbar相关，里面的item则不管
<template>
  <div id="tab-bar"> 
      <slot></slot>
    </div>
</template>
<script>
export default {
  name:'TabBar',
}
</script>
<style>
  #tab-bar{
  display: flex;
  background-color: #f6f6f6;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  box-shadow: 0px -1px 1px rgba(100, 100, 100, .2);
}
</style>