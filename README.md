# dialog-helper ![](https://img.shields.io/badge/license-MIT-F44336.svg)

## 背景

在做业务代码的modal弹窗时，总是围绕visible变量以及控制visible变量逻辑，能否简化弹窗相关逻辑呢？


## Install

``` bash
npm i dialog-helper
```

## Quick Start

Import modules and set up settings in main.js:

``` js
import ElDialogHelper from 'dialog-helper'
Vue.use(ElDialogHelper)
```

use `Vue.prototype.$openDialog` in your App.vue

``` vue
<template>
  <el-button type="primary" @click="open" size="small">编程式打开dialog</el-button>
</template>

<script>
import ElDialog from "./elementui-dialog";
export default {
  methods: {
    open() {
      this.$openDialog(ElDialog)({ name: "123" })
        .then(() => this.$message.success('任务成功'))
        .catch(() => this.$message.warning('任务失败'));
    }
  }
};
</script>
```

use `Vue.prototype.$closeDialog` in your elementui-dialog.vue:

``` vue
<template>
  <el-dialog title="ElementUI Dialog" :visible.sync="visible">
    {{ name }}
    <div>
      <el-button type="primary" @click="$closeDialog(true)">确定</el-button>
      <el-button @click="$closeDialog(false)">取消</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  props: { name: String },
  data() {
    return { visible: false };
  }
};
</script>
```

## API

### 1. Vue.prototype.$openDialog()

使用方式：`this.$openDialog(DialogComponent)(props = {}, parentContext = undefined)`

* DialogComponent： 自定义的弹窗.vue组件

* props：弹窗组件需要传入的初始化props

* parentContext：弹窗的父级上下文，一般用于获取父级 provider， 如获取 ConfigProvider 的配置、$store、$router

返回等待用户弹窗关闭的Promise，当Dialog弹窗组件`$emit('done')`时，resolve promise；当`$emit('cancel')`时，reject promise。

### 2. Vue.prototype.$closeDialog()

使用方式： this.$closeDialog(isSuccess = false, ...args)

全局注入的快捷方法，`是$emit('done')和$emit('cancel')的快捷键`。当isSuccess = true，执行$emit('done');当isSuccess = false时，执行$emit('cancel')。
