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
      label="作品提交截止日期"
      width="180"
    >
      <template slot-scope="scope">
        <i class="el-icon-time" />
        <span style="margin-left: 10px">{{ scope.row.date }}</span>
      </template>
    </el-table-column>
    <el-table-column
      prop="request"
      label="要求"
    />
    <el-table-column
      :filters="[{ text: '已提交', value: '已提交' }, { text: '未提交', value: '未提交' }]"
      :filter-method="filterTag"
      prop="tag"
      label="状态"
      width="100"
      filter-placement="bottom-end"
    >
      <template slot-scope="scope">
        <el-tag
          :type="scope.row.tag === '未提交' ? 'primary' : 'success'"
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
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          v-if="scope.row.tag === '未提交' && scope.row.stage === '未评审'"
          size="mini"
          @click="handleSubmit(scope.$index, scope.row)"
        >提交</el-button>
        <el-button
          v-else-if="scope.row.tag === '已提交' && scope.row.stage === '已评审'"
          size="mini"
          @click="handleCheckResult(scope.$index, scope.row)"
        >查看</el-button>
        <el-button
          v-else
          size="mini"
          @click="handleWait(scope.$index, scope.row)"
        >等待评审</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '数学竞赛',
        request: '提交pdf',
        tag: '已提交',
        stage: '已评审'
      }, {
        date: '2016-05-04',
        name: '英语竞赛',
        request: '提交png',
        tag: '未提交',
        stage: '未评审'
      }, {
        date: '2016-05-01',
        name: '化学竞赛',
        request: '提交压缩包',
        tag: '已提交',
        stage: '未评审'
      }, {
        date: '2016-05-03',
        name: '物理竞赛',
        request: '提交mp4',
        tag: '未提交',
        stage: '未评审'
      }]
    }
  },
  methods: {
    handleSubmit(index, row) {
      console.log(index, row)
    },
    handleCheckResult(index, row) {
      console.log(index, row)
    },
    handleWait(index, row) {
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
