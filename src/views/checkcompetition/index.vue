<template>
  <el-table
    ref="filterTable"
    :data="tableData"
    style="width: 100%"
  >
    <el-table-column
      prop="name"
      label="竞赛名"
      width="180"
    />
    <el-table-column
      label="竞赛类型"
      width="180"
    >
      <template slot-scope="scope">
        <i class="el-icon-time" />
        <span style="margin-left: 10px">{{ scope.row.type }}</span>
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
        type: '数学',
        name: '数学竞赛',
        request: '提交pdf',
        tag: '已提交',
        stage: '已评审'
      }, {
        type: '英语',
        name: '英语竞赛',
        request: '提交png',
        tag: '未提交',
        stage: '未评审'
      }, {
        type: '化学',
        name: '化学竞赛',
        request: '提交压缩包',
        tag: '已提交',
        stage: '未评审'
      }, {
        type: '物理',
        name: '物理竞赛',
        request: '提交mp4',
        tag: '未提交',
        stage: '未评审'
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
