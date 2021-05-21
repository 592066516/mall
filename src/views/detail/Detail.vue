<template>
    <div id="detail">
        <DetailNavBar></DetailNavBar>
        <DetailSwiper :topImages="topImages"></DetailSwiper>
        <DetailBaseInfo :goods="Goods"></DetailBaseInfo>
    </div>
</template>
<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from '@/views/detail/childComps/DetailSwiper'
import DetailBaseInfo from '@/views/detail/childComps/DetailBaseInfo'

import {getDetail,Goods} from "network/detail" 
export default {
  name: "Detail",
  components:{
      DetailNavBar,
      DetailSwiper,
      DetailBaseInfo
  },
  data() {
    return {
      iid: null,
      topImages:[],
      Goods:null
    };
  },
  created() {
    // 保存传入的id
    this.iid = this.$route.params.iid;
    // 2.根据iid请求详情数据
    getDetail(this.iid).then(res=>{
      console.log(res)
      const data = res.result
      this.topImages = data.itemInfo.topImages
      // 2.获取商品信息
      this.Goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)

    })

  }
};
</script>
<style>
</style>


