<template>
  <div id="home">
    <nav-bar class="home-nav">
      <!-- 第一种写法 -->
      <!-- <div slot="center">购物街</div> -->
      <!-- 第二种写法 -->
      <!-- <template v-slot:center>购物街</template> -->
      <!-- 简写 -->
      <template #center>购物街</template>
    </nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feautre-view></feautre-view>


    <ul>
      <li>
        列表1
        列表2
        列表3
        列表4
        列表5
        列表6
        列表7
        列表8
        列表9
        列表10
        列表11
        列表12
        列表13
        列表14
        列表15
        列表16
        列表17
        列表18
        列表19
        列表20
        列表21
        列表22
        列表23
        列表24
        列表25
        列表26
        列表27
        列表28
        列表29
        列表30
        列表31
        列表32
        列表33
        列表34
        列表35
        列表36
        列表37
        列表38
        列表39
        列表40
        列表41
        列表42
        列表43
        列表44
        列表45
        列表46
        列表47
        列表48
        列表49
        列表50
        列表51
        列表52
        列表53
        列表54
        列表55
        列表56
        列表57
        列表58
        列表59
        列表60
        列表61
        列表62
        列表63
        列表64
        列表65
        列表66
        列表67
        列表68
        列表69
        列表70
        列表71
        列表72
        列表73
        列表74
        列表75
        列表76
        列表77
        列表78
        列表79
        列表80
        列表81
        列表82
        列表83
        列表84
        列表85
        列表86
        列表87
        列表88
        列表89
        列表90
        列表91
        列表92
        列表93
        列表94
        列表95
        列表96
        列表97
        列表98
        列表99
        列表100
      </li>
    </ul>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeautreView from "./childComps/FeautreView";

import { getHomeMultidata } from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeautreView
  },
  data() {
    return {
      banners: [],
      recommends: []
    };
  },
  created() {
    // 1.请求多个数据
    getHomeMultidata().then(res => {
      console.log(res);

      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  }
};
</script>

<style scoped>
#home {
  padding-top: 44px;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9;
}
</style>
