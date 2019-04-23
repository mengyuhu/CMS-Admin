<template>
  <el-table
    :data="tableData"
    style="width: 100%"
  >

    <el-table-column
      label="竞赛名"
      width="180"
    >
      <template slot-scope="scope">
        <el-popover trigger="hover" placement="top">
          <p>竞赛名: {{ scope.row.name }}</p>
          <p>简介: {{ scope.row.summary }}</p>
          <div slot="reference" class="name-wrapper">
            <el-tag size="medium">{{ scope.row.name }}</el-tag>
          </div>
        </el-popover>
      </template>
    </el-table-column>
    <el-table-column
      prop="summary"
      label="简介"
    />
    <el-table-column
      label="报名截止日期"
      width="180"
    >
      <template slot-scope="scope">
        <i class="el-icon-time" />
        <span style="margin-left: 10px">{{ scope.row.date }}</span>
      </template>
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)"
        >报名</el-button>
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
        summary: '关于数学的竞赛'
      }, {
        date: '2016-05-04',
        name: '英语竞赛',
        summary: '关于英语的竞赛'
      }, {
        date: '2016-05-01',
        name: 'c语言竞赛',
        summary: '关于c语言编程的竞赛'
      }, {
        date: '2016-05-03',
        name: 'ACM大赛',
        summary: '编程比赛'
      }]
    }
  },
  methods: {
    handleEdit(index, row) {
      console.log(index, row)
    }
  }
}
</script>
