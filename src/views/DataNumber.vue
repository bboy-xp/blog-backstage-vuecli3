<template>
  <div class="dataNumberContent">
    <el-container>
      <el-header>博客后台</el-header>
      <el-container>
        <el-aside width="200px">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo">
            <el-menu-item index="1" @click="gotoHome">
              <i class="el-icon-edit"></i>
              <span slot="title">数据管理</span>
            </el-menu-item>
            <el-menu-item index="2">
              <i class="el-icon-edit"></i>
              <span slot="title">数据总览</span>
            </el-menu-item>
          </el-menu>
        </el-aside>
        <el-main>
          <el-row>
            <el-col :span="10">
              <div id="myChart" class="grid-content bg-purple-dark">
                总数：100
              </div>
            </el-col>
          </el-row>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data() {
    return {
      myChart: null,
      option: []
    };
  },
  mounted() {
    this.drawLine();
  },
  methods: {
    gotoHome() {
      this.$router.push({ path: "/" });
    },
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById("myChart"));

      this.option = {
        title: {
          text: "一周访问量"
        },
        tooltip: {
          trigger: "axis"
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            name: "访问人数",
            type: "line",
            stack: "总量",
            data: [80, 122, 101, 204, 90, 170, 130]
          }
        ]
      };
      // 绘制图表
      myChart.setOption(this.option);
    }
  }
};
</script>

<style scoped>
.homeContent {
  height: 100%;
  width: 100%;
  /* overflow: scroll; */
}
.el-header {
  text-align: center;
  line-height: 60px;
  color: #333;
  font-size: 3vw;
}
.grid-content {
  border-radius: 4px;
  height: 500px;
}
.bg-purple-dark {
  /* background: #99a9bf; */
}
</style>