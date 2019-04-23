<template>
  <el-form ref="form" :model="form" label-width="80px">
    <el-form-item label="竞赛名称">
      <el-input v-model="form.name" />
    </el-form-item>
    <el-form-item label="竞赛类型">
      <el-select v-model="form.type" placeholder="请选择竞赛类型">
        <el-option label="数学" value="math" />
        <el-option label="英语" value="english" />
        <el-option label="化学" value="chemistry" />
        <el-option label="物理" value="physics" />
        <el-option label="编程" value="programming" />
      </el-select>
    </el-form-item>
    <el-form-item label="报名截止日期">
      <el-col :span="11">
        <el-date-picker v-model="form.date1" type="date" placeholder="选择日期" style="width: 100%;" />
      </el-col>
    </el-form-item>
    <el-form-item label="作品提交截止日期">
      <el-col :span="11">
        <el-date-picker v-model="form.date2" type="date" placeholder="选择日期" style="width: 100%;" />
      </el-col>
    </el-form-item>
    <el-form-item label="评审截止日期">
      <el-col :span="11">
        <el-date-picker v-model="form.date3" type="date" placeholder="选择日期" style="width: 100%;" />
      </el-col>
    </el-form-item>
    <el-form-item label="作品格式">
      <el-checkbox-group v-model="form.workType">
        <el-checkbox label="pdf" name="type" />
        <el-checkbox label="mp4" name="type" />
        <el-checkbox label="png" name="type" />
        <el-checkbox label="zip" name="type" />
        <el-checkbox label="word" name="type" />
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="简介">
      <el-input v-model="form.desc" type="textarea" />
    </el-form-item>
    <el-form-item>
      <el-upload
        class="upload-demo"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :before-remove="beforeRemove"
        multiple
        :limit="3"
        :on-exceed="handleExceed"
        :file-list="form.fileList"
      >
        <el-button size="small" type="primary">上传评审标准与资质文件</el-button>
        <div slot="tip" class="el-upload__tip">只能上传txt文件，且不超过500kb</div>
      </el-upload>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">申请发布</el-button>
      <el-button @click="onDelete">取消</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        type: '',
        date1: '',
        date2: '',
        date3: '',
        workType: [],
        desc: '',
        fileList: [{ name: '评审标准.jpeg', url: '@/评分标准.txt' }]
      }
    }
  },
  methods: {
    onSubmit() {
      console.log('submit!')
    },
    onDelete() {
      console.log('delete!')
    },
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePreview(file) {
      console.log(file)
    },
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`)
    },
    beforeRemove(file, fileList) {
      return this.$confirm(`确定移除 ${file.name}？`)
    }
  }
}
</script>
