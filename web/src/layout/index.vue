<template>
  <el-container>
    <el-aside :width.sync="width">
      <Aside :width.sync="width"></Aside>
    </el-aside>
    <el-container>
      <el-header>
        <Header></Header>
      </el-header>
      <el-main>
        <Main></Main>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Header from "./modules/Header";
import Main from "./modules/Main";
import Aside from "./modules/Aside";
import store from "../store";
import routers from "../router/routers";
export default {
  name: "index",
  components: {
    Header,
    Main,
    Aside
  },
  beforeMount() {
    //  页面刷新后,清空所有的已打开的tab(如果想保留之前的记录，可以不清空)
    store.dispatch('clearTabAction')
    //  然后将首页保存进已打开的tab列表中
    store.dispatch('addTabAction', {path: '/home', name: '首页'})
    //  并将首页设计为激活值
    store.dispatch('activeIndexAction', '首页')
    //  最后打开首页
    routers.push({path: '/home'})
  },
  data(){
    return{
      width: '230px'
    }
  }
}
</script>

<style scoped>
  .el-aside{
    height: calc(100vh);
  }
  .el-header{
    display: flex;
    align-items: center;
  }
  .el-main{
    padding: 0;
  }
</style>