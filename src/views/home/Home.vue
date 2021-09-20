<template>
  <div id="home">
    <NavBar class="home-nav"><div slot="center">购物街</div></NavBar>
    <HomeSwiper :banners="banners"></HomeSwiper>
    <RecommendView :recommends="recommend"></RecommendView>
  </div>

</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  import HomeSwiper from "views/home/childComps/HomeSwiper";
  import RecommendView from "views/home/childComps/RecommendView";

  import {getHomeMultidata} from "network/home";

  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      RecommendView
    },
    data() {
      return {
        banners: [],
        recommend: []
      }
    },
    created() {
      //1.请求多个数据
      getHomeMultidata().then(res => {
        console.log(res);
        this.banners = res.data.banner.list;
        this.recommend = res.data.recommend.list;
      })
    }
  }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }
</style>
