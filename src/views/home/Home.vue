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
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import { getHomeMultidata } from "network/home";
export default {
  name: "Home",
  components: {
    NavBar
  },
  data(){
    return {
      result:null,
    }
  },
  created() {
    // 1.请求多个数据
    getHomeMultidata().then(res=>{
      console.log(res);
      
      this.result = res
 
     
    })
  }
};
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
}
</style>
