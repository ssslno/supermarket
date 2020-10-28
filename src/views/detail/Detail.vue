<template>
<div id="detail">
    <detail-nav-bar></detail-nav-bar>
    <detail-swiper :top-images="topImages"></detail-swiper>
</div>
  
</template>

<script>
import DetailNavBar from "./childComps/DetailNavBar"
import {getDetail,Goods} from "network/detail.js"
import DetailSwiper from "./childComps/DetailSwiper"
export default {
    name:'Detail',
    components:{
        DetailNavBar,
        DetailSwiper

    },
   
    data(){
        return {
            iid:null,
            topImages:[]
        }
    },
    created(){
        //保存传入的iid
        this.iid = this.$route.params.iid
        //根据iid请求详情数据 做一层封装
        getDetail(this.iid).then(res=>{
            console.log(res);
            const data =res.result;
            this.topImages = res.result.itemInfo.topImages
            //获取商品信息 
            this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)
         
        })

    }

}
</script>

<style scoped>

</style>