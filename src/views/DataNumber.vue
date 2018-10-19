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
              <div class="grid-content bg-purple-dark">
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
    return {};
  },
  methods: {
    gotoHome() {
      this.$router.push({ path: "/" });
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
  height: 40px;
}
.bg-purple-dark {
  /* background: #99a9bf; */
}
</style>