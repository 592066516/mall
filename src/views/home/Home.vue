<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <Scroll
      class="content"
      ref="scroll"
      :probe-type="3"
      :pull-up-load="true"
      @scroll="contentscroll"
      @pullingUp="loadMore"
    >
      <!-- 轮播图组件 -->
      <HomeSwiper :banners="banners"></HomeSwiper>
      <HomeRecommendView :recommends="recommends"></HomeRecommendView>
      <FeatureView></FeatureView>
      <TabControl class="tab-control" :titles="['流行','新款','精选']" @tabClick="tabClick"></TabControl>

      <GoodsList :goods="showGoods"></GoodsList>
    </Scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"/>
  </div>
</template>




<script>
import HomeSwiper from "./childComps/HomeSwiper";
import HomeRecommendView from "./childComps/HomeRecommendView";
import FeatureView from "./childComps/FeatureView";

import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import Scroll from "components/common/scroll/Scroll";
import BackTop from "components/content/backTop/BackTop";

import { getHomeMultidata, getHomeGoods } from "network/home";
import { debounce } from "common/utils";

export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    HomeSwiper,
    HomeRecommendView,
    FeatureView,
    GoodsList,
    Scroll,
    BackTop
  },
  data() {
    return {
      banners: [],
      recommends: [],
      // 自定义Goods商品数据
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        seil: { page: 0, list: [] }
      },
      currentType: "pop",
      isShowBackTop: false
    };
  },
  // 计算属性
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    }
  },
  created() {
    // 1.请求多个数据
    this.getHomeMultidata();
    // 2.请求商品数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("seil");
  },
  mounted() {
    const refresh = debounce(this.$refs.scroll.refresh, 50);

    // 3.监听item图片加载完成
    this.$bus.$on("itemImageLoad", () => {
      refresh();
      // this.$refs.scroll.refresh();
    });
  },
  methods: {
    // 事件监听相关的方法
    tabClick(index) {
      console.log(index);
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "seil";
      }
    },
    backClick() {
      console.log("点击上箭头回到顶部");
      this.$refs.scroll.scroll.scrollTo(0, 0);
    },

    loadMore() {
      console.log("加载更多");
      this.getHomeGoods(this.currentType);
    },
    // loadMore() {
    //   console.log("上拉加载更多");
    //   this.getHomeGoods(this.currentType);

    //   this.$refs.scroll.scroll.refresh();
    // },
    contentscroll(position) {
      // y 负值   加括号转为正值
      this.isShowBackTop = -position.y > 2000;
    },
    // 网络请求相关的方法
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        // 完成上拉加载更多
        this.$refs.scroll.finishPullUp();
      });
    }
  }
};
</script>

<style scoped>
#home {
  padding-top: 44px;
  height: 100vh;
  position: relative;
}

.home-nav {
  background-color: var(--color-tint);
  color: #fff;

  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}

.tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
}

.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}

/*.content {*/
/*height: calc(100% - 93px);*/
/*overflow: hidden;*/
/*margin-top: 44px;*/
/*}*/
</style>
