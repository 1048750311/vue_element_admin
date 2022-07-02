<template>
  <div class="app-container">
    <el-card>
      <!-- 搜索与添加区域 -->
      <el-row :gutter="20">
        <el-col :span="5">
          <el-input placeholder="请输入内容" v-model="search" clearable @clear="getUserList">
            <el-button slot="append" icon="el-icon-search" @click="getUserList"></el-button>
          </el-input>
        </el-col>
        <el-col :span="2">
          <el-button type="primary">查询用户</el-button>
        </el-col>
        <el-col :span="2">
          <el-button type="danger" @click="delAll">强退所有用户</el-button>
        </el-col>
      </el-row>
    </el-card>
    <!--表格渲染-->
    <el-table ref="table" :data="dataList" style="width: 100%;">
      <el-table-column type="selection" width="55" />
      <el-table-column prop="ou_id" label="ID" />
      <el-table-column prop="ou_title" label="用户名" />
      <el-table-column prop="ou_name" label="用户昵称" />
      <el-table-column prop="ou_department" label="部门" />
      <el-table-column prop="ou_ip" label="登录IP" />
      <el-table-column :show-overflow-tooltip="true" prop="ou_location" label="登录地点" />
      <el-table-column prop="ou_time" label="登录时间" />
      <el-table-column label="操作" width="70px" fixed="right">
        <template slot-scope="scope">
          <el-button slot="reference" size="mini" type="text" @click="delMethod(scope.row.ou_id, scope.$index)">强退
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
// import CRUD, { presenter, header, crud } from '@crud/crud'

export default {
  name: 'OnlineUser',
  data() {
    return {
      delLoading: false,
      permission: {},
      search: '',
      dataList: [{
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '36.170.59.114',
        ou_location: '中国',
        ou_time: '2022/6/2 00:37:48',
        ou_id: 1
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '11.22.33.44',
        ou_location: '中国四川成都',
        ou_time: '2022/6/2 00:37:48',
        ou_id: 2
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '153.154.156.15',
        ou_location: '韩国',
        ou_time: '2022/6/2 00:37:48',
        ou_id: 3
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '52.244.230.26',
        ou_location: '中国四川成都',
        ou_time: '2022/6/2 00:37:48',
        ou_id: 4
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '210.28.61.83',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 5
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '117.245.31.25',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 6
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '131.107.110.167',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 7
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '3.82.51.102',
        ou_location: '中国深圳',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 8
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '14.175.229.239',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 9
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '112.241.106.248',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 10
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '115.217.172.102',
        ou_location: '中国',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 11
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '56.77.223.165',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 12
      },
      {
        ou_title: 'admin',
        ou_name: '管理员',
        ou_department: '研发部',
        ou_ip: '232.221.245.142',
        ou_location: '中国四川成都',
        ou_time: '2022/6/1 12:37:48',
        ou_id: 13
      }

      ]
    }
  },
  mounted() {
  },
  methods: {
    doDelete(datas) {
      this.$confirm(`确认强退选中的${datas.length}个用户?`, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        console.log('deleteyes')
      })
    },
    getData() {
      return {
        code: 20000,
        data: []
      }
    },

    // 踢出用户
    delMethod(key, index) {
      console.log(key, index)
      this.dataList.splice(index, 1)
      this.$message({
        message: '删除成功',
        type: 'success'
      })
    },

    delAll() {
      this.dataList = []
      this.$message({
        message: '全部删除成功',
        type: 'success'
      })
    }
  }
}
</script>
