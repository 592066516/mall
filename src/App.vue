<template>
  <div id="app">
    <router-view/>
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
