<template>
  <div class="homeContent">
    <el-container>
      <el-header>博客后台</el-header>
      <el-container>
        <el-aside width="200px">
          <el-menu
            default-active="1"
            class="el-menu-vertical-demo">
            <el-menu-item index="1">
              <i class="el-icon-edit"></i>
              <span slot="title">数据管理</span>
            </el-menu-item>
            <el-menu-item index="2" @click="gotoDataNumber">
              <i class="el-icon-edit"></i>
              <span slot="title">数据总览</span>
            </el-menu-item>
          </el-menu>
        </el-aside>
        <el-main>
          <!-- <el-table
            :data="tableData"
            stripe
            style="width: 100%">
            <el-table-column
              prop="createdAt"
              label="日期"
              >
            </el-table-column>
            <el-table-column
              prop="author"
              label="作者"
              >
            </el-table-column>
            <el-table-column
              prop="title"
              label="标题">
            </el-table-column>
            <el-table-column
              prop="content"
              label="内容">
            </el-table-column>
            <el-table-column label="操作">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleDelete(scope.$index, scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table> -->

          <el-table
            :data="tableData"
            style="width: 100%">
            <el-table-column type="expand">
              <template slot-scope="props">
                <el-form label-position="left" inline class="demo-table-expand">
                  <el-row>
                    <el-col :span="8">
                      <el-form-item label="日期">
                        <span>{{ props.row.createdAt }}</span>
                      </el-form-item>
                    </el-col>
                    <el-col :span="8">
                      <el-form-item label="作者">
                        <span>{{ props.row.author }}</span>
                      </el-form-item>
                    </el-col>
                    <el-col :span="8">
                      <el-form-item label="标题">
                        <span>{{ props.row.title }}</span>
                      </el-form-item>
                    </el-col>
                  </el-row>
                  <el-form-item label="内容">
                    <div class="contentText">{{ props.row.content }}</div>
                  </el-form-item>
                </el-form>
              </template>
            </el-table-column>
            <el-table-column
              label="日期"
              prop="date">
            </el-table-column>
            <el-table-column
              label="作者"
              prop="author">
            </el-table-column>
            <el-table-column
              label="标题"
              prop="title">
            </el-table-column>
            <el-table-column label="操作">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleDelete(scope.$index, scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  data() {
    return {
      tableData: []
    };
  },
  methods: {
    gotoDataNumber() {
      this.$router.push({ path: "/dataNumber" });
    },
    async handleDelete(index, row) {
      // console.log(row._id);
      const id = row._id;
      const deleteBlog = await axios.post("http://127.0.0.1:7001/deleteArticle", {id: id});
      // console.log(deleteBlog);
      this.tableData = deleteBlog.data;
    }
  },
  async mounted() {
    const allData = await axios.get("http://127.0.0.1:7001/getArticle");
    // const allData = await axios.post("http://127.0.0.1:7001/article",{});
    this.tableData = allData.data;
    console.log(this.tableData);
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
.contentText {
  width: 80%;
  word-wrap: break-word;
}
</style>

