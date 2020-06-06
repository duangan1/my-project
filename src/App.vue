<template>
  <div id="app">
    <img src="./assets/logo.png">
      <li><router-link  to="test">欢迎来到test</router-link></li>
      <li><router-link  to="/" >欢迎来到菜鸟教程</router-link></li>
    <router-view></router-view> 

    <!-- router-view显示的是当前路由地址所对应的内容 -->
    <!-- 不想跳转到新页面，只在当前页面切换着显示，那么就要涉及到路由的嵌套 -->
  <!-- <fenshitu></fenshitu> -->
  </div>
</template>


<script>
// import fenshitu from './components/fenshitu'
export default {
  name: 'App',
  components: {
    // fenshitu,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
