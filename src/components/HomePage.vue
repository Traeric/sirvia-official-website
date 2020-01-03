<template>
    <div>
        <div id="top">
            <div class="left">
                <div class="logo">
                    <img src="../assets/images/logo.png" alt="NO IMG">
                </div>
            </div>
            <div class="right">

            </div>
        </div>
        <div id="bottom">
            <div class="left">
                <div class="select-version">
                    <h2>版本</h2>
                    <el-select v-model="selectVersion" placeholder="活动区域">
                        <el-option label="区域一" value="0"></el-option>
                        <el-option label="区域二" value="1"></el-option>
                    </el-select>
                </div>
                <div class="title"><h2>目录</h2></div>
                <div class="menu">
                    <el-menu
                            default-active="2"
                            class="el-menu-vertical-demo"
                            @open="handleOpen"
                            @close="handleClose">
                        <el-submenu index="1">
                            <template slot="title">
                                <i class="el-icon-location"></i>
                                <span>导航一</span>
                            </template>
                            <el-menu-item-group>
                                <template slot="title">分组一</template>
                                <el-menu-item index="1-1">选项1</el-menu-item>
                                <el-menu-item index="1-2">选项2</el-menu-item>
                            </el-menu-item-group>
                            <el-menu-item-group title="分组2">
                                <el-menu-item index="1-3">选项3</el-menu-item>
                            </el-menu-item-group>
                            <el-submenu index="1-4">
                                <template slot="title">选项4</template>
                                <el-menu-item index="1-4-1">选项1</el-menu-item>
                            </el-submenu>
                        </el-submenu>
                        <el-menu-item index="2">
                            <i class="el-icon-menu"></i>
                            <span slot="title">导航二</span>
                        </el-menu-item>
                        <el-menu-item index="3" disabled>
                            <i class="el-icon-document"></i>
                            <span slot="title">导航三</span>
                        </el-menu-item>
                        <el-menu-item index="4">
                            <i class="el-icon-setting"></i>
                            <span slot="title">导航四</span>
                        </el-menu-item>
                    </el-menu>
                </div>
            </div>
            <div class="right"></div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                selectVersion: "0",
            };
        },
    }
</script>

<style scoped>
    #top {
        height: 60px;
        border-bottom: 1px solid #ececec;
        overflow: hidden;
    }

    #top .left .logo {
        height: 50px;
        margin-top: 5px;
        margin-left: 50px;
    }

    #top .left .logo img {
        height: 100%;
    }

    #top .left {
        float: left;
    }

    #top .right {
        float: right;
    }

    #bottom {
        display: flex;
    }

    #bottom .left {
        margin: 20px 10px;
    }

    #bottom .left .select-version {
        display: flex;
        align-content: center;
        justify-content: center;
    }

    #bottom .left .select-version h2 {
        margin: 3px 10px 0 0;
    }

    #bottom .left .title {
        text-align: left;
        margin-top: 20px;
    }

    #bottom .left .menu {text-align: left; margin-top: 10px;}
</style>