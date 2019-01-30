<template>
    <div class="hn-login">
        <el-card class="hn-login-card">
            <div slot='header'>管理员登录</div>
            <div>
                <el-form>
                    <el-form-item label="管理员名：" label-width="100px">
                        <el-input v-model="formData.aname" placeholder="请输入管理员名"></el-input>
                    </el-form-item>

                    <el-form-item label="登录密码：" label-width="100px">
                        <el-input v-model="formData.apwd" type="password" placeholder="请输入登录密码"></el-input>
                    </el-form-item>

                    <el-form-item label-width="100px">
                        <!-- 非button元素，单击事件必须加.native -->
                        <el-button type="primary" @click="doLogin">登录</el-button>
                        <el-button @click="doCancel">取消</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </el-card>
    </div>
</template>
<script>
export default {
    data(){//普通组件的模型数据是函数的返回值
        return {
            formData:{
                aname:'admin',
                apwd:'123456'
            }
        }
    },
    methods:{
        doLogin(){
            var url = this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`
            this.$axios.get(url).then((result)=>{
                if(result.data.code==200){//登录成功
                    // 把用户名存入Vuex存储仓库
                    this.$store.commit('setAdminName',this.formData.aname)
                    // 执行视图跳转
                    this.$router.push('/main')
                }else{//登录失败
                    this.$alert('用户名或者密码有误！','登录失败',{type:'error'}).then().catch(()=>{})
                }
            }).catch((err)=>{
                console.log(err)
            })
        },
        doCancel(){
            this.formData.aname='';
            this.formData.apwd=''
        }
    }
}
</script>

<style lang="scss">
.hn-login{
    .hn-login-card{
        width: 400px;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%);
        .el-card__header{
            text-align: center;
        }
    }
}
</style>
