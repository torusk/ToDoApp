<template>
  <div>
    <h1>issueリスト</h1>
    <el-button type="success" @click="getIssues()">issue取得</el-button>
    <el-row :gutter="12">
      <!-- コード１ -->
      <el-col :span="12" v-for="issue in issues" :key="issue.id">
        <el-card class="box-card" shadow="hover" style="margin: 5px 0">
          <el-row :gutter="12">
            <!-- コード2 -->
            <el-col :span="21">{{ issue.title }}</el-col>
            <el-col :span="3">
              <el-button type="success" icon="el-icon-check" circle></el-button>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios"; // --1

const client = axios.create({
  //--1
  baseURL: "https://api.github.com/repos/diveintocode-corp/vue_seriese_api", //--2
  headers: {
    //--3
    Accept: "application/vnd.github.v3+json",
    "Content-Type": "application/json",
  },
});

export default {
  name: "IssueList",
  data() {
    return {
      issues: [],
    };
  },
  methods: {
    getIssues() {
      client
        .get("/issues") //--4
        .then((res) => {
          this.issues = res.data;
        });
    },
  },
};
</script>
