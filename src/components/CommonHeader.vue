<template>
  <header>
    <div class="l-content">
      <el-button plain icon="el-icon-menu" size="mini" @click="handlerMenu"></el-button>
      <breadcrumb id="breadcrumb-container" class="breadcrumb-container" />
      <!-- <h3 style="color:#fff">首页</h3> -->
    </div>
    <div class="r-content">
      <NowDate/>
      <Screenfull id="screenfull" class="right-menu-item hover-effect" />
      <el-dropdown trigger="click" size="mini">
        <span>
          <img class="user" :src="userImg" />
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>个人中心</el-dropdown-item>
          <el-dropdown-item @click.native="$router.push('/Welcome')">首页</el-dropdown-item>
          <el-dropdown-item>退出</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </header>
</template>
<script>
import Screenfull from './Screenfull/index.vue'
import Breadcrumb from './Breadcrumb/index.vue'
import NowDate from './NowDate/index.vue'
export default {
  name: 'CommonHeader',
  components: {
    Screenfull,
    Breadcrumb,
    NowDate
  },
  data() {
    return {
      userImg: require('../assets/images/eva.jpg')
    }
  },
  methods: {
    handlerMenu() {
      this.$store.commit('collapseMenu')
    }
  }
}
</script>
<style lang="less" scoped>
header {
  display: flex;
  height: 100%;
  justify-content: space-between;
  align-items: center;
}

.l-content {
  display: flex;
  align-items: center;

  .el-button {
    margin-right: 20px;
  }
}
.breadcrumb-container {
    float: left;
  }
.r-content {
  line-height: 60px;
  display:flex;
  .user {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
}
.right-menu-item {
      display: inline-block;
      padding: 0 8px;
      height: 100%;
      font-size: 18px;
      color: #5a5e66;
      vertical-align: middle;

      &.hover-effect {
        cursor: pointer;
        transition: background .3s;

        &:hover {
          background: rgba(0, 0, 0, .025)
        }
      }
    }
</style>
