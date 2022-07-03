<template>
  <el-menu background-color="#545c64" text-color="#fff" active-text-color="#ffd04b" class="el-menu-vertical-demo"
    @open="handleOpen" @close="handleClose" :collapse="isCollapse" router :default-active="activePath">
    <h3>{{ isCollapse ? '后台' : '智能设备管理后台' }}</h3>
    <!-- :index="item.path+''"记得加+''变字符串 -->
    <el-menu-item index="/Welcome" @click.native="saveNavState('/Welcome')">
      <i class="el-icon-menu"></i>
      <span slot="title">首页</span>
    </el-menu-item>
    <el-submenu :index="item.id + ''" v-for="item in menulist" :key="item.id">
      <!-- 一级菜单的模板区域 -->
      <template slot="title">
        <!-- 图标 -->
        <i :class="iconsObj[item.id]"></i>
        <!-- 文本 -->
        <span>{{ item.authName }}</span>
      </template>

      <!-- 二级菜单 -->
      <el-menu-item :index="'/' + subItem.path" v-for="subItem in item.children" :key="subItem.id"
        @click="saveNavState('/' + subItem.path)">
        <template slot="title">
          <!-- 图标 -->
          <i class="el-icon-menu"></i>
          <!-- 文本 -->
          <span>{{ subItem.authName }}</span>
        </template>
      </el-menu-item>
    </el-submenu>
  </el-menu>
</template>
<script>
export default {
  name: 'NavMenu',
  data() {
    return {
      menu: [],
      menulist: [],
      iconsObj: {
        '125': 'iconfont icon-user',
        '103': 'iconfont icon-tijikongjian',
        '160': 'iconfont icon-tijikongjian',
        '101': 'iconfont icon-shangpin',
        '102': 'iconfont icon-danju',
        '145': 'iconfont icon-baobiao'
      },
      activePath: ''
    }
  },
  created() {
    this.getMenuList()
    this.activePath = window.sessionStorage.getItem('activePath')
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath)
    },
    logout() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    async getMenuList() {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
      this.menulist = res.data
      console.log(res)
    },
    // 保存链接的激活状态
    saveNavState(activePath) {
      window.sessionStorage.setItem('activePath', activePath)
      this.activePath = activePath
    }
  },
  computed: {
    isCollapse() {
      return this.$store.state.tab.isCollapse
    }
  }
}
</script>
<style lang="less" scoped>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}

.el-menu {
  height: 100%;
  border: none;

  h3 {
    color: #fff;
    text-align: center;
    line-height: 48px;
  }
}
</style>
