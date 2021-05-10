<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <!-- 轮播图组件 -->
   <HomeSwiper :banners="banners"></HomeSwiper>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from 'views/home/childComps/HomeSwiper' 

import { getHomeMultidata } from "network/home";



export default {
  name: "Home",
  components: {
    NavBar,
   
    HomeSwiper
  },
  data() {
    return {
      banners: [],
      recommends:[]
    };
  },
  created() {
    // 请求多个数据
    getHomeMultidata().then(res => {
      this.banners = res.data.banner.list;
      console.log(this.banners)
      this.recommends = res.data.recommend.list;
    });
  }
};
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
}
</style>
