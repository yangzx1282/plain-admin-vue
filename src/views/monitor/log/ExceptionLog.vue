<template>
  <div>
    <el-card>
      <search-bar :searchForm="searchForm" @search-click="searchHandler"></search-bar>
      <el-row>
        <!-- 使用组件的形式 -->
        <data-table ref="dataTable" :API="API" :logType="logType" :searchForm="searchForm">
          
        </data-table>
      </el-row>
    </el-card>
    
  </div>
</template>

<script>
import DataTable from "./LogTable"
export default {
  data() {
    return {
      // 搜索表单
      searchForm: {
        word: null,
        startTime: null,
        endTime: null,
        status: null,
      },
      API: this.$api.LOG_API,
      logType: "ERROR",
    }
  },
  methods: {
    searchHandler(formData) {
      if (formData.dateScope != null) {
        this.searchForm.startTime = formData.dateScope[0];
        this.searchForm.endTime = formData.dateScope[1];
      } else {
        this.searchForm.startTime = null;
        this.searchForm.endTime = null;
      }
      // return
      this.$refs.dataTable.queryHandler(1);
    },
  },
  mounted() {
    // console.log(this.API)
    console.log(this.$slots)
  },
  components: { DataTable }
};
</script>

<style>
  
</style>
