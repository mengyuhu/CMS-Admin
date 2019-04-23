<template>
  <el-table
    ref="filterTable"
    :data="tableData"
    style="width: 100%"
  >
    <el-table-column
      prop="name"
      label="用户名"
      width="180"
    />
    <el-table-column
      label="个人简介"
      width="180"
    >
      <template slot-scope="scope">
        <i class="el-icon-time" />
        <span style="margin-left: 10px">{{ scope.row.brief }}</span>
      </template>
    </el-table-column>
    <el-table-column label="检查资质">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleDownload(scope.$index, scope.row)"
        >资质文件</el-button>
      </template>
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleAgree(scope.$index, scope.row)"
        >通过</el-button>
        <el-button
          size="mini"
          @click="handleRefuse(scope.$index, scope.row)"
        >拒绝</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [{
        brief: '数学竞赛举办方',
        name: '十七中学'
      }, {
        brief: '英语竞赛举办方',
        name: '电子科大'
      }, {
        brief: '化学竞赛举办方',
        name: '东南大学'
      }, {
        brief: '物理竞赛举办方',
        name: '北大'
      }]
    }
  },
  methods: {
    handleAgree(index, row) {
      console.log(index, row)
    },
    handleRefuse(index, row) {
      console.log(index, row)
    },
    handleDownload(index, row) {
      console.log(index, row)
    },
    resetDateFilter() {
      this.$refs.filterTable.clearFilter('date')
    },
    clearFilter() {
      this.$refs.filterTable.clearFilter()
    },
    formatter(row, column) {
      return row.address
    },
    filterTag(value, row) {
      return row.tag === value
    },
    filterHandler(value, row, column) {
      const property = column['property']
      return row[property] === value
    }
  }
}
</script>
