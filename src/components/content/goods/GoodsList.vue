<template>
  <div class="goods">
    <GoodsListItem v-for="item in goods" :key="item.id" :goods-item="item"></GoodsListItem>
  </div>
</template>

<script>
import GoodsListItem from "./GoodsListItem";

export default {
  name: "GoodsList",
  components: {
    GoodsListItem
  },
  props: {
    goods: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style scoped>
.goods {
  display: flex;
  /* 让弹性盒元素在必要的时候拆行： */
  flex-wrap: wrap;
 /* 项目位于各行之前、之间、之后都留有空白的容器内 */
  justify-content: space-around;
  padding: 2px;
}
</style>
