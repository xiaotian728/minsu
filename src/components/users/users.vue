<template>
<el-card class="box-card">
    <!-- 面包屑 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">

        <el-breadcrumb-item>用户管理</el-breadcrumb-item>
        <el-breadcrumb-item>用户列表</el-breadcrumb-item>
        <el-breadcrumb-item>活动详情</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 搜索 -->
    <el-row class="searchRow">
        <el-col>
            <el-input placeholder="请输入内容" v-model="query" class="inputSearch">

                <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
            <el-button type="success">添加用户</el-button>
        </el-col>
    </el-row>
    <!-- 表格 -->
    <el-table :data="userlist" style="width: 100%">
        <el-table-column type="index" label="#" width="60">
        </el-table-column>
        <el-table-column prop="username" label="姓名" width="80">
        </el-table-column>
        <el-table-column prop="email" label="邮箱">
        </el-table-column>
        <el-table-column prop="mobile" label="电话">
        </el-table-column>
        <el-table-column label="创建时间">
            <!-- 如果单元格内显示内容不是字符串（文本），
            需要给被现实的内容外包一个template -->

            <!-- template内部使用数据，设置slot-scope属性，
            改属性是要用数据的数据源userlist
             -->

            <!-- slot-scope的字userlist其实就是el-table绑定的数据userlist 
             userlist-row->数组中的每个对象
             -->
            <template slot-scope="userlist">
                {{userlist.row.create_time | fmtdate}}
            </template>

        </el-table-column>
        <el-table-column label="用户状态">
            <template slot-scope="scope">
                <el-switch v-model="scope.row.mg_state" active-color="#13ce66" inactive-color="#ff4949">
                </el-switch>
            </template>
        </el-table-column>
        <el-table-column prop="address" label="操作">
            <template slot-scope="scope">

                <el-button size="mini" plain type="primary" icon="el-icon-edit" circle></el-button>
                <el-button size="mini" plain type="success" icon="el-icon-check" circle></el-button>
                <el-button size="mini" plain type="danger" icon="el-icon-delete" circle></el-button>
            </template>
        </el-table-column>
    </el-table>

</el-card>
</template>

<script>
export default {
    data() {
        return {
            query: '',
            //表格绑定数据
            pagenum: 1,
            //分页相关数据
            total: -1,
            pagesize: 2,
            userlist: [],

        }
    },
    created() {
        this.getUserList()
    },
    methods: {
        async getUserList() {
            //query查询参数可为空
            //pagenum 当前页码不为空
            //pagesize 每页显示条数，不为空
            //需要授权api，必须在请求头中使用Authorization字段提供token令牌
            const AUTH_TOKEN = localStorage.getItem('token')
            this.$http.defaults.headers.common['Authorization'] = AUTH_TOKEN;
            const res = await this.$http.get(
                `users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${
                    this.pagesize 
                 }`
            )
            console.log(res)
            const {
                meta: {
                    status,
                    msg
                },
                data: {
                    users,
                    total
                }
            } = res.data
            if (status === 200) {
                //给表格数据赋值
                this.userlist = users
                //total赋值
                this.total = total
                //以及提示
                this.$message.success(msg)
            } else {
                this.$message.error();
                (msg)
            }

        }
    }
}
</script>

<style>
.box-card {
    height: 100%;
}

.inputSearch {
    width: 300px;
}

.searchRow {
    margin-top: 20px;
}
</style>
