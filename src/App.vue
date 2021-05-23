<template>
  <div id="app">
    <!-- keep-alive 防止组件再次渲染  销魂 -->
    <!-- exclude="Detail" 属性 让itemgoods点击跳转详情页iid不为1 -->
    <keep-alive exclude="Detail">
        <router-view/>
    </keep-alive>
   
    <main-tab-bar class="tab"/>
  </div>
</template>

<script>
  import MainTabBar from 'components/content/mainTabbar/MainTabBar'

  export default {
    name: 'app',
    components: {
      MainTabBar
    }
  }
</script>

<style>
  @import "assets/css/base.css";
  .tab{
    z-index: 999;
  }
</style>
