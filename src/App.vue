<template>
  <div id="app">
    <!--header-->
    <app-header :poiInfo="poiInfo"></app-header>
    <!--nav-->
    <app-nav :commentNum="commentNum"></app-nav>

    <!--content-->
    <!--keep-alive可以在切换路由后保证数据不改变-->
    <keep-alive>
        <router-view></router-view>
    </keep-alive>
    

  </div>
</template>

<script>
import Header from './components/header/Header'
import Nav from './components/nav/Nav'
export default {
  name: 'App',
  data(){
    return{
      poiInfo:{},
      commentNum:0,
    }
  },
  components:{
    "app-header":Header,
    "app-nav":Nav
  },
  created(){
    // axios
    // fetch
    fetch("api/goods")
    .then(res=>{
      return res.json()
    })
    .then(res=>{
      // console.log(res);
      if(res.code==0){
        this.poiInfo=res.data.poi_info;
        // console.log(this.poiInfo);
      }
    })

    // 请求ratings
    fetch("api/ratings")
    .then(res=>{
      return res.json()
    })
    .then(res=>{
      // console.log(res);
      if(res.code==0){
        this.commentNum=res.data.comment_num;
        // console.log(this.poiInfo);
      }
    })
  }
}
</script>

<style>

</style>
