<template>
    <div>
        欢迎回来：{{this.$store.state.adminName}}
        <div>MAIN 左边栏目</div>
        <div>MAIN 顶部提示</div>
        <router-view></router-view>
    </div>
</template>
<script>
export default {
    data(){
        return {
            aname:this.$store.state.adminName
        }
    }
}
</script>
