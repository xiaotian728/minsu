<template>
<el-container class="container">
    <el-header class="header">
        <el-row>
            <el-col :span="4">
                <div class="grid-content bg-purple">
                    <img src="../../assets/logo.jpeg" alt="无法显示图片" width="100px" height="60px">
                </div>
            </el-col>
            <el-col :span="18" class="middle">

                <h3>民宿租赁管理平台</h3>
            </el-col>
            <el-col :span="2">
                <div class="grid-content bg-purple">
                    <a class="loginout" @click.prevent="handleSignout()" href="#">退出</a>
                </div>
            </el-col>
        </el-row>
    </el-header>
    <el-container>
        <el-aside class="aside" width="200px">
            <el-menu :unique-opened="true">
                <!-- 1 -->
                <el-submenu index="1">
                    <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>用户管理</span>
                    </template>

                    <!-- <template slot="title">分组一</template> -->
                    <el-menu-item index="1-1">
                        <i class="el-icon-s-flag"></i>
                        <span>用户列表</span>
                    </el-menu-item>

                </el-submenu>
                <!-- 2 -->
                <el-submenu index="2">
                    <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>权限管理</span>
                    </template>

                    <!-- <template slot="title">分组一</template> -->
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>角色列表</span>
                    </el-menu-item>
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>权限列表</span>
                    </el-menu-item>
                </el-submenu>
                <!-- 3 -->
                <el-submenu index="3">
                    <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>商品管理</span>
                    </template>

                    <!-- <template slot="title">分组一</template> -->
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>商品列表</span>
                    </el-menu-item>
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>商品分类</span>
                    </el-menu-item>
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>分类参数</span>
                    </el-menu-item>
                </el-submenu>
                <!-- 4 -->
                <el-submenu index="4">
                    <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>订单管理</span>
                    </template>

                    <!-- <template slot="title">分组一</template> -->
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>订单列表</span>
                    </el-menu-item>

                </el-submenu>
                <!-- 5 -->
                <el-submenu index="5">
                    <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>数据统计</span>
                    </template>

                    <!-- <template slot="title">分组一</template> -->
                    <el-menu-item index="1-1">
                        <i class="el-icon-location"></i>
                        <span>数据图表展示</span>
                    </el-menu-item>

                </el-submenu>

            </el-menu>
        </el-aside>
        <el-main class="main">Main</el-main>
    </el-container>
</el-container>
</template>

<script>
export default {
    beforeCreate() {
        // 获取token
        const token = localStorage.getItem('token')
        //if token 有->继续渲染组件
        if (!token) {
            this.$router.push({
                name: 'login'
            })
        }
        //token 无->登录
        //newVue前自动触发

    },
    methods:{
        handleSignout(){
            //清除token
            localStorage.clear()
            //提示
            this.$message.success('退出成功')
            //来到login组件
            this.$router.push({name:'login'})
        }
    }
}
</script>

<style>
.container {
    height: 100%;
}

.header {
    background-color: #a2bcdd;
}

.aside {
    background-color: #f0f2f3;
}

.main {
    background-color: #5e93c9;
    height: 100%;
}

.middle {
    text-align: center;
}

.loginout {

    line-height: 60px;
    text-decoration: none;
}
</style>
