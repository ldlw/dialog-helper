<template>
  <div id="app">
    <el-button type="primary" @click="open" size="small">编程式打开ElementUI Dialog</el-button>

    <el-button type="primary" @click="openAntdv" size="small">编程式打开Antdv Dialog</el-button>
  </div>
</template>

<script>
import ElDialog from './elementui-dialog';
import AdDialog from './antd-dialog'
export default {
  name: 'app',
  methods: {
    open() {
      this.$openDialog(ElDialog)({ name: '123' })
        .then(() => this.$message.success('任务成功'))
        .catch(() => this.$message.warning('任务失败'));
    },
    openAntdv() {
      this.$openDialog(AdDialog)({ name: '123' })
        .then(() => this.$message.success('任务成功'))
        .catch(() => this.$message.warning('任务失败'));
    }
  }
};
</script>
