<template>
    <!-- 头部区域 -->
    <el-container class="home-container">
        <el-header>
            <div class="left-logo">
                <img src="../assets/logo.png"/>
                <span 
                    ><h3>停车场管理系统</h3>
                </span>
            </div>
            <div style="text-align: right;width: 50%;padding-right: 25px;">

              欢迎使用，{{ userInfo.nike }}
            </div>
            <el-button type="danger" icon="iconfont icon-r-left" @click="logout"> 退出登录</el-button>
        </el-header>
        <!-- 页面主体区域 -->
        <el-container>
            <!-- 侧边栏 -->
            <el-aside width="auto">
                <el-menu
                    background-color="white"
                    text-color="black"
                    active-text-color="grey"
                    :unique-opened="true"
                    :collapse-transition="false"
                    router
                    :default-active="activePath"
                >
                    <!-- 菜单 -->
                    <el-menu-item
                        :index="item.path + ''"
                        v-for="item in menuList"
                        :key="item.id"
                        @click="savePath('/' + item.path)"
                        
                    >
                        <template slot="title">
                            <i :class="item.icon" style="font-size: 28px;color: black;"></i>
                            <span><b style="font-size: 18px;"> {{ item.name }}</b></span>
                        </template>
                    </el-menu-item>
                </el-menu>
            </el-aside>
            <!-- 右侧内容主体 -->
            <el-main>
                <!-- 路由占位符 -->
                <router-view></router-view>
            </el-main>
        </el-container>
    </el-container>
</template>
<script>
import axios from "axios";
export default {
    data() {
        return {
            menuList: [
                {
                    name: "首页",
                    id: 101,
                    path: "maneHome",
                    icon: "iconfont icon-r-home",
                },
                {
                    name: "用户信息管理",
                    id: 111,
                    path: "userMane",
                    icon: "iconfont icon-r-user1",
                },
                {
                    name: "车位信息管理",
                    id: 131,
                    path: "carmaneger",
                    icon: "iconfont icon-r-building",
                },
                {
                    name: "车位费用设置",
                    id: 141,
                    path: "money",
                    icon: "iconfont icon-r-shield",
                },
                {
                    name: "停泊车辆查询",
                    id: 151,
                    path: "stallMane",
                    icon: "iconfont icon-r-find",
                },
                {
                    name: "车辆进出管理",
                    id: 161,
                    path: "carInMane",
                    icon: "iconfont icon-r-right",
                },
                {
                    name: "登录日志查询",
                    id: 171,
                    path: "loginInfoMane",
                    icon: "iconfont icon-r-paper",
                },
            ],
            userInfo: {},
            activePath: "/users",
        };
    },
    created() {
        this.activePath = window.sessionStorage.getItem("savePath");
    },
    methods: {
        getUserInfo() {
            const uid = window.sessionStorage.getItem("token");
            axios.get("/api/user/getUserByUid?uid=" + uid).then((res) => {
                this.userInfo = res.data.data;
            });
        },
        logout() {
            window.sessionStorage.clear();
            this.$router.push("/login");
            this.$message("您已退出登录，请重新登录！");
        },
        savePath(savePath) {
            window.sessionStorage.setItem("savePath", savePath);
        },
    },
    mounted() {
        this.getUserInfo();
    },
};
</script>
<style scoped>
.home-container {
    height: 100%;
}
.el-header {
    background-color: white;
    display: flex;
    justify-content: space-between;
    padding-left: 0;
    align-items: center;
    color: black;
    font-size: 20px;
    border-bottom: 1px solid grey;
}
.left-logo {
    height: 100%;
    display: flex;
    align-items: center;
}
.left-logo > span {
    margin-left: 15px;
}
.left-logo > img {
    height: 50%;
    margin-left: 25px;
}
.el-aside {
    background-color: white;
}
.el-main {
    background-color: #eaedf1;
}
.el-menu {
    border-right: none;
}
.fa {
    margin-right: 10px;
}
.toggle-button {
    background-color: #4a5064;
    font-size: 10px;
    line-height: 24px;
    color: #fff;
    text-align: center;
    letter-spacing: 0.2em;
    cursor: pointer;
}
</style>