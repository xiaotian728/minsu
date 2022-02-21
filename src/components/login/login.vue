<template>
<div class="login-wrap">
    <el-form 
    class="login-form"
    label-position="top" 
    label-width="80px" 
    :model="fromdata">
    <h2>管理员登录</h2>
       <el-form-item label="用户名">
          <el-input v-model="fromdata.username"></el-input>
       </el-form-item>
       <el-form-item label="密码">
          <el-input v-model="fromdata.password"></el-input>
       </el-form-item>
        <el-button 
        @click.prevent="handleLogin"
        class="login-btn" type="primary">登录</el-button>
    </el-form>
</div>
</template>
<script>
export default {
    data() {
        return {
            fromdata:{
                username: '',
                password: ''
            }
        }
    },
    methods: {
     async handleLogin() {
         //异步操作转为同步，async和await的使用
        const res = await this.$http.post('login',this.fromdata)
            // console.log(res)
            const {
                data,meta:{msg,status}
            } = res.data
            if (status === 200) {
                this.$router.push({name:"home"})
                //成功提示
                this.$message.success(msg);
            }else {
                this.$message.warning(msg)
            }
            
        }
    }
}


</script>
<style>
.login-wrap{
  height: 100%;
  background-color: #24374d;
  display: flex;
  justify-content: center;
  align-items: center ;
}
.login-wrap .login-form{
    background-color: #fff;
    width: 400px;
    border-radius: 5px;
    padding:30px;
}
.login-wrap .login-btn{
    width: 100%;
}
</style>
