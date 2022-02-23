一．	登录
1.	应用第三方插件axios
Axios插件baseurl=http://localhost:8888/api/private/v1/
2.	登录组件login.vue中登录成功，msg=登陆成功从何处定义的
if (status === 200) {
             //  this.$router.push({name:home})
                //成功提示
                this.$message.success(msg);
3.	路由跳转---容器---组件---配置路由—挂在路由
（1）．js编程式导航
（2）app.Vue router -view
(3)新建home组件
（4）路由index.js配置路由
4,异步操作变同步 es7 
5.不让用户通过url直接进入url（不登录），登陆成功时保存正确用户的token
 
二．	Home
1.	头部首部调整：
2.	侧边栏：router是否开启路由模式
        unique-opened	是否只保持一个子菜单的展开
3.	调整element -ui（index值不能一样，否则目标不明确，点击一个联动）
4.	进入首页的权限验证
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

    }
三．	用户列表
1.	home。vue列表开启路由模式
2.	main-》router-view
3.	新建users。Vue
4.	Router/index.js在home中children配置user的路由
四、面包屑和搜索框
  1.el-card卡片容器
  2.面包屑
  3.el-row>el-rol>el-input-button
4.调整样式
五．引入表格table
1.el-table(data数据源[]) > el-table-column(lable 表头/prop=”数据”) >字符串数据
2.el-table属性中type=“index”单元格内容从1开始
3.重点：请求`users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${
                    this.pagesize 
                 }`注意双引号
4.用户请求数据-设置请求头
  （1）created（）{this.getUserList()}
   (2)methods:{getUserList(){发送请求}}
  （3）接口文档中除了登录之外的素偶有请求都需要进行授权---设置请求头
  （4）找axios中关于请求头的设置代码
     this.$http.defaults.headers.common['Authorization'] = AUTH_TOKEN;
