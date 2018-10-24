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
                <el-button
                  size="mini"
                  type="primary"
                  @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
              </template>
            </el-table-column>
          </el-table>

          <!-- editModel -->
          <el-dialog title="编辑博客" :visible.sync="dialogEditVisible">
            <el-row>
              <el-col>
                <span>作者</span>
                <el-input maxlength="30" v-model="input" :placeholder="this.placeholderData.author"></el-input>
              </el-col>
              <el-col class="editBox">
                <span>标题</span>
                <el-input maxlength="30" v-model="input" :placeholder="this.placeholderData.title"></el-input>
              </el-col>
              <el-col class="editBox">
                <span>内容</span>
                <el-input maxlength="30" v-model="input" :placeholder="this.placeholderData.content"></el-input>
              </el-col>
              <el-col class="editBox">
                <span>ObjectId</span>
                <span class="el-input">{{this.placeholderData._id}}</span>
              </el-col>
            </el-row>
          </el-dialog>
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
      tableData: [],
      dialogEditVisible: false,
      input: "",
      placeholderData: {
        _id: "5ba9fc587bad274a84977ead",
        title: "sefesfse",
        author: "fsefsef",
        content : "12312312312"
      }
    };
  },
  methods: {
    gotoDataNumber() {
      this.$router.push({ path: "/dataNumber" });
    },
    async handleDelete(index, row) {
      // console.log(row._id);
      const id = row._id;
      const deleteBlog = await axios.post(
        "http://127.0.0.1:7001/deleteArticle",
        { id: id }
      );
      // console.log(deleteBlog);
      this.tableData = deleteBlog.data;
    },
    async handleEdit(index, row) {
      // console.log(row);
      this.placeholderData = row;
      this.dialogEditVisible = !this.dialogEditVisible;
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
.el-input {
  width: 300px;
  margin-left: 40px;
}
.editBox {
  margin-top: 20px;
}
</style>

