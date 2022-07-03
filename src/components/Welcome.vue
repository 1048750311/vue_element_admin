<template>
  <el-row class="home" :gutter="20">
    <el-col :span="8" style="margin-top: 20px">
      <el-card shadow="hover">
        <div class="user">
          <img :src="userImg" />
          <div class="userInfo">
            <p class="name">{{ username }}</p>
          </div>
        </div>
        <div class="login-info">
          <p>上次登录时间:<span>2021-7-19</span></p>
          <p>上次登录地点:<span>芜湖</span></p>
        </div>
      </el-card>
      <el-card style="margin-top: 20px; height: 460px" shadow="hover">
        <!-- 下方注入data对象数组 -->
        <el-table :data="tableData">
          <el-table-column v-for="(item, key) in tableLabel" :key="key" :prop="key" :label="item"> </el-table-column>
        </el-table>
      </el-card>
    </el-col>
    <el-col style="margin-top: 20px" :span="16">
      <div class="num">
        <!-- 注意flex布局 -->
        <el-card class="noBorder" v-for="item in countData" :key="item.name"
          :body-style="{ display: 'flex', padding: 0 }" shadow="hover">
          <i class="icon" :class="`el-icon-${item.icon}`" :style="{ background: item.color }"></i>
          <div class="detail">
            <p class="num">￥{{ item.value }}</p>
            <p class="txt">{{ item.name }}</p>
          </div>
        </el-card>
      </div>

      <el-card style="height: 280px" shadow="hover">
        <!-- <div style="height:280px" ref="echarts"></div> -->
        <echart :chartData="echartData.order" style="height: 280px" />
      </el-card>

      <div class="graph">
        <el-card style="height: 260px" shadow="hover">
          <!-- <div style="height:240px" ref="userEcharts"></div> -->
          <echart :chartData="echartData.user" style="height: 240px" />
        </el-card>

        <el-card style="height: 260px" shadow="hover">
          <!-- <div style="height:240px" ref="videoEcharts"></div> -->
          <!-- :isAxisChart="false"表示不是折线图 -->
          <echart :chartData="echartData.video" :isAxisChart="false" style="height: 240px" />
        </el-card>
      </div>
    </el-col>
  </el-row>
</template>
<script>
import Echart from './Echarts.vue'
import Mock from 'mockjs'
export default {
  name: 'home',
  components: {
    Echart
  },
  data() {
    return {
      activeIndex: '1',
      activeIndex2: '1',
      username: '',
      userImg: require('../assets/images/eva.jpg'),
      tableData: [],
      tableLabel: {
        name: '课程',
        todayBuy: '今日购买',
        monthBuy: '本月购买',
        totalBuy: '总购买'
      },
      countData: [
        {
          name: '今日支付订单',
          value: 34,
          icon: 'success',
          color: '#2ec7c9'
        },
        {
          name: '今日收藏订单',
          value: 210,
          icon: 'star-on',
          color: '#ffb980'
        },
        {
          name: '今日未支付订单',
          value: 1234,
          icon: 's-goods',
          color: '#5ab1ef'
        },
        {
          name: '本月支付订单',
          value: 1224,
          icon: 'success',
          color: '#2ec7c9'
        },
        {
          name: '本月收藏订单',
          value: 739,
          icon: 'star-on',
          color: '#ffb980'
        },
        {
          name: '本月未支付订单',
          value: 15,
          icon: 's-goods',
          color: '#5ab1ef'
        }
      ],
      echartData: {
        order: {
          xData: [],
          series: []
        },
        user: {
          xData: [],
          series: []
        },
        video: {
          series: []
        }
      }
    }
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath)
    },
    getEchartData() {
      let List = []
      for (let i = 0; i < 7; i++) {
        List.push(
          Mock.mock({
            苹果: Mock.Random.float(100, 8000, 0, 0),
            vivo: Mock.Random.float(100, 8000, 0, 0),
            oppo: Mock.Random.float(100, 8000, 0, 0),
            魅族: Mock.Random.float(100, 8000, 0, 0),
            三星: Mock.Random.float(100, 8000, 0, 0),
            小米: Mock.Random.float(100, 8000, 0, 0)
          })
        )
      }
      return {
        code: 20000,
        data: {
          // 饼图
          videoData: [
            {
              name: '小米',
              value: 2999
            },
            {
              name: '苹果',
              value: 5999
            },
            {
              name: 'vivo',
              value: 1500
            },
            {
              name: 'oppo',
              value: 1999
            },
            {
              name: '魅族',
              value: 2200
            },
            {
              name: '三星',
              value: 4500
            }
          ],
          // 柱状图
          userData: [
            {
              date: '周一',
              new: 5,
              active: 200
            },
            {
              date: '周二',
              new: 10,
              active: 500
            },
            {
              date: '周三',
              new: 12,
              active: 550
            },
            {
              date: '周四',
              new: 60,
              active: 800
            },
            {
              date: '周五',
              new: 65,
              active: 550
            },
            {
              date: '周六',
              new: 53,
              active: 770
            },
            {
              date: '周日',
              new: 33,
              active: 170
            }
          ],
          // 折线图
          orderData: {
            date: ['20191001', '20191002', '20191003', '20191004', '20191005', '20191006', '20191007'],
            data: List
          },
          tableData: [
            {
              name: 'oppo',
              todayBuy: 500,
              monthBuy: 3500,
              totalBuy: 22000
            },
            {
              name: 'vivo',
              todayBuy: 300,
              monthBuy: 2200,
              totalBuy: 24000
            },
            {
              name: '苹果',
              todayBuy: 800,
              monthBuy: 4500,
              totalBuy: 65000
            },
            {
              name: '小米',
              todayBuy: 1200,
              monthBuy: 6500,
              totalBuy: 45000
            },
            {
              name: '三星',
              todayBuy: 300,
              monthBuy: 2000,
              totalBuy: 34000
            },
            {
              name: '魅族',
              todayBuy: 350,
              monthBuy: 3000,
              totalBuy: 22000
            }
          ]
        }
      }
    }
  },
  mounted() {
    this.username = window.sessionStorage.getItem('username')
    let EchartData = this.getEchartData()
    const { code, data } = EchartData
    if (code === 20000) {
      this.tableData = data.tableData
      const order = data.orderData
      const xData = order.date
      const keyArray = Object.keys(order.data[0])
      const series = []
      keyArray.forEach((key) => {
        series.push({
          name: key,
          data: order.data.map((item) => item[key]),
          type: 'line'
        })
      })
      this.echartData.order.xData = xData
      this.echartData.order.series = series

      this.echartData.user.xData = data.userData.map((item) => item.date)
      this.echartData.user.series = [
        {
          name: '新增用户',
          data: data.userData.map((item) => item.new),
          type: 'bar'
        },
        {
          name: '活跃用户',
          data: data.userData.map((item) => item.active),
          type: 'bar'
        }
      ]

      this.echartData.video.series = [
        {
          data: data.videoData,
          type: 'pie'
        }
      ]
    }
  }
}
</script>
<style lang="less" scoped>
.home {
  .user {
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    margin-bottom: 20px;
    border-bottom: 1px solid #ccc;

    img {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      margin-right: 40px;
    }

    &info {
      .name {
        font-size: 32px;
        margin-bottom: 10px;
      }

      .access {
        color: #999999;
      }
    }
  }

  .login-info {
    p {
      line-height: 28px;
      font-size: 14px;
      color: #999999;

      span {
        color: #666666;
        margin-left: 60px;
      }
    }
  }

  .num {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;

    .el-card {
      width: 32%;
      margin-bottom: 20px;
    }

    .icon {
      font-size: 30px;
      width: 80px;
      height: 80px;
      text-align: center;
      line-height: 80px;
      color: #fff;
    }

    .detail {
      margin-left: 15px;
      display: flex;
      flex-direction: column;
      justify-content: center;

      .num {
        font-size: 30px;
        margin-bottom: 10px;
      }

      .txt {
        font-size: 14px;
        text-align: center;
        color: #999999;
      }
    }
  }

  .graph {
    margin-top: 20px;
    display: flex;
    justify-content: space-between;

    .el-card {
      width: 48%;
    }
  }
}

.noBorder {
  border: none !important;
}
</style>
