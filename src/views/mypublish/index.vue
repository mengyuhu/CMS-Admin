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
      :filters="[{ text: '审核中', value: '审核中' }, { text: '通过', value: '通过' }, { text: '未通过', value: '未通过' }]"
      :filter-method="filterTag"
      prop="tag"
      label="状态"
      width="100"
      filter-placement="bottom-end"
    >
      <template slot-scope="scope">
        <el-tag
          :type="scope.row.tag === '审核中' ? 'primary' : (scope.row.tag ==='通过' ? 'success' : 'danger')"
          disable-transitions
        >{{ scope.row.tag }}</el-tag>
      </template>
    </el-table-column>
    <el-table-column
      :filters="[{ text: '已评审', value: '已评审' }, { text: '未评审', value: '未评审' }]"
      :filter-method="filterTag"
      prop="stage"
      label="阶段"
      width="100"
      filter-placement="bottom-end"
    >
      <template slot-scope="scope">
        <el-tag
          :type="scope.row.stage === '未评审' ? 'primary' : 'success'"
          disable-transitions
        >{{ scope.row.stage }}</el-tag>
      </template>
    </el-table-column>
    <el-table-column label="评分表">
      <template slot-scope="scope">
        <el-button
          v-if="scope.row.stage ==='已评审'"
          size="mini"
          @click="handleDownload(scope.$index, scope.row)"
        >下载</el-button>
        <el-button
          v-else
          size="mini"
          @click="handleWaitResult(scope.$index, scope.row)"
        >等待评审</el-button>
      </template>
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          v-if="scope.row.tag === '通过' && scope.row.stage === '已评审' && !scope.row.submitted"
          size="mini"
          @click="handleSubmit(scope.$index, scope.row)"
        >提交获奖名单</el-button>
        <el-button
          v-else-if="scope.row.tag === '通过' && scope.row.stage === '未评审' && !scope.row.submitted"
          size="mini"
          @click="handleWait(scope.$index, scope.row)"
        >等待评审</el-button>
        <el-button
          v-else-if="scope.row.tag === '审核中' && scope.row.stage === '未评审' && !scope.row.submitted"
          size="mini"
          @click="handleWaitCheck(scope.$index, scope.row)"
        >等待审核</el-button>
        <el-button
          v-else-if="scope.row.tag === '未通过' && scope.row.stage === '未评审' && !scope.row.submitted"
          size="mini"
          @click="reapply(scope.$index, scope.row)"
        >重新申请</el-button>
        <el-button
          v-else-if="scope.row.tag === '通过' && scope.row.stage === '已评审' && scope.row.submitted"
          size="mini"
          @click="handleResult(scope.$index, scope.row)"
        >已提交结果</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [{
        name: '数学竞赛',
        tag: '审核中',
        stage: '未评审',
        submitted: false
      }, {
        name: '英语竞赛',
        tag: '通过',
        stage: '未评审',
        submitted: false
      }, {
        name: '化学竞赛',
        tag: '未通过',
        stage: '未评审',
        submitted: false
      }, {
        name: '物理竞赛',
        tag: '通过',
        stage: '已评审',
        submitted: false
      }, {
        name: '编程竞赛',
        tag: '通过',
        stage: '已评审',
        submitted: true
      }]
    }
  },
  methods: {
    handleSubmit(index, row) {
      console.log(index, row)
    },
    handleResult(index, row) {
      console.log(index, row)
    },
    handleWait(index, row) {
      console.log(index, row)
    },
    handleWaitCheck(index, row) {
      console.log(index, row)
    },
    handleDownload(index, row) {
      console.log(index, row)
    },
    handleWaitResult(index, row) {
      console.log(index, row)
    },
    reapply(index, row) {
      console.log(index, row)
    }, // //////////////////////////////////////////////////////////////
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
