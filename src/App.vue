<template>
  <div id="app">
    <!-- 容器 -->
    <router-view/>
  </div>
</template>
<script>
export default {
  mounted(){
      //当前组件挂载完成后，异步请求全局设置
      var url=this.$store.state.globalSettings.apiUrl+`/admin/settings`
      this.$axios.get(url).then((result)=>{
          this.$store.commit('setGlobalSettings',result.data)
      }).catch((err)=>{
          console.log(err)
      })
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  color: #303133;
}
</style>
