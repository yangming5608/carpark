<!--
 * @Description: 
 * @Author: Rabbiter
 * @Date: 2023-09-01 09:55:21
-->
<template>
    <div>
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item><i
                    class="iconfont icon-r-home"
                    style="margin: 5px; font-size: 22px"
                >
                    首页</i></el-breadcrumb-item>
        </el-breadcrumb>
        <el-row style="background-color: white;padding: 0 0 50px 25px;">

            <el-col :span="24" style="font-size: 24px; text-align: left;">
                <h1>欢迎访问停车场管理系统</h1>
            </el-col>

            <el-col :span="24" style="text-align: left;">
                <img :src="require('@/assets/img/03.jpg')" style="height: 50vh;">
            </el-col>
        </el-row>
    </div>
</template>
<script>
export default {
    data() {
        return {
            
        };
    },
    methods: {
        
    },
    mounted() {
        
    },
};
</script>
<style scoped>

</style>