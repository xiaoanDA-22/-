<template>
    <div class="common-layout">
      <el-container class="box">
        <!-- 左侧菜单栏 -->
        <el-aside class="el-aside">
          <h1 class="logoBox">后台管理系统</h1>
          <el-menu
            active-text-color="#ffd04b"
            background-color="#545c64"
            class="el-menu-vertical-demo"
            default-active="2"
            text-color="#fff"
            @open="handleOpen"
            @close="handleClose"
            :router="true">

            <template v-for="item in asideMenu">
              <!-- 两级菜单 -->
              <template v-if="item.subs">
                <el-sub-menu :index="item.title" :key="item.title">
                  <!-- 一级菜单标题 -->
                  <template #title>
                    <el-icon><document /></el-icon>
                    <span>{{ item.title }}</span>
                  </template>
                  <!-- 二级菜单标题 -->
                  <template v-for="subItem in item.subs" :key="subItem.index">
                    <el-menu-item
                      :index="subItem.index"
                      @click="() => handleMenuItem(subItem)">
                      {{ subItem.title }}</el-menu-item>
                  </template>
                </el-sub-menu>
              </template>

              <template v-else>
                <el-menu-item
                    :index="item.index"
                    :key="item.title"
                    @click="() => handleMenuItem(item)">
                    <el-icon><document /></el-icon>
                    <span>{{ item.title }}</span>
                  </el-menu-item>
              </template>
          </template>

          </el-menu>
        </el-aside>
   
        <el-container>
          <!-- header头部菜单 -->
          <el-header class="header"> <!-- main主体模块：标签页 + 当前路由内容 -->
            <el-menu
              class="el-menu-demo"
              mode="horizontal"
              background-color="#545c64"
              text-color="#fff"
              active-text-color="#ffd04b">
              <el-menu-item index="1" class="fr">张家铖</el-menu-item>
              <el-sub-menu index="2" class="fr">
                <template #title class="fr">我的工作台</template>
                <el-menu-item index="2-1">我的消息</el-menu-item>
                <el-menu-item index="2-2">设置</el-menu-item>
                <el-menu-item index="2-3" @click="exitLogin">退出登陆</el-menu-item>
              </el-sub-menu>
            </el-menu>
          </el-header>
          <el-main class="el-main"> 
            
          </el-main>
        </el-container>
      </el-container>
    </div>
</template>
   
<script>
import {
  Document,
  Menu as IconMenu,
  Location,
  Setting,
} from '@element-plus/icons-vue'
import { ElMessageBox } from "element-plus";
export default {
  name: "Main",
  mounted() {
  },
  data() {
    return {
      //当前选项卡
      activeTabName: "home",
      //需要显示的标签数组
      editableTabs: [
        {
          title: "首页",
          index: "home",
        },
      ],
      //左侧菜单选项配置
      asideMenu: [
        {
          title: "用户",
          index: "user",
        },
        {
          title: "文章",
          subs: [
            {
              title: "文章列表",
              index: "articleList",
            },
          ],
        },
        {
          title: "测试",
          index: "test",
        },
      ],
    };
  },
  components: {
    Document,
    IconMenu,
    Location,
    Setting,
  },
  watch: {
    activeTabName: function () {
      console.log("高亮的index值", this.activeTabName);
    },
  },
  methods:{
    handleMenuItem(obj) {
      //高亮设置
      this.activeTabName = obj.index;
      let result = this.editableTabs.findIndex((item) => {
        return item.index == obj.index;
      });
      if (result != -1) {
        return;
      }
      this.editableTabs.push(obj);
    },
  },
};
</script>

  <style scoped>
  .logoBox {
    position: absolute;
    top: 18px;
    left: 30px;
    font-size: 24px;
    color: #fff;
  }
   
  .box {
    width: 100vw;
    height: 100vh;
  }
  .header {
    padding: 0;
    height: 58px;
    background-color: #545c64;
  }
   
   
  /* 去除默认的边框样式 */
  .el-header .el-menu {
    border-bottom: none;
  }
  .el-aside .el-menu {
    border-right: none;
  }
   
  .el-main {
    background-color: #e9eef3;
  }
   
  .el-aside {
    width: 240px;
    background: #545c64;
    padding-top: 58px;
  }

  /* 将消息中心和我的控制台摆放在最右侧 */
  .el-menu--horizontal {
    justify-content: flex-end;
  }
  </style>