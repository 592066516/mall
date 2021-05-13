<template>
    <!-- <div class="back-top" @click="backclick">
        <img src="~assets/img/common/top.png" alt="">
    </div> -->
    <div class="back-top">
        <img src="~assets/img/common/top.png" alt="">
    </div>
</template>
<script>
export default {
    name:"BackTop",
    // methods:{
    //     backclick(){
    //         // 将事件抛射出去，在父组件使用
    //         this.$emit('backclick')
    //     }
    // }
}
</script>
<style>
.back-top{
    position: fixed;
    bottom: 60px;
    right: 10px;


}
.back-top img {
    width: 43px;
    height: 43px;
}
</style>


