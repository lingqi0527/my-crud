![](https://raw.githubusercontent.com/d2-projects/d2-crud/master/doc/image/banner.png)

![npm](https://img.shields.io/npm/v/@d2-projects/d2-crud.svg)
![npm](https://img.shields.io/npm/dt/@d2-projects/d2-crud.svg)
![GitHub license](https://img.shields.io/github/license/d2-projects/d2-crud.svg)


## 介绍

[D2-Crud](https://github.com/d2-projects/d2-crud)基于D2-Crud修改的vue组件，添加部分功能。

## 功能

- 继承了 Element 中表格所有功能
- 新增表格数据
- 修改表格数据
- 删除表格数据
- 使用 Element 中的组件渲染表格内容和表单内容
- 表单校验
- 表格内编辑
- 渲染自定义组件

## 安装

使用npm
``` bash
npm i element-ui my-element-crud -S
```

## 在项目中使用

在`main.js`中写入以下内容：

``` js
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import D2Crud from 'my-element-crud'

Vue.use(ElementUI)
Vue.use(D2Crud)

new Vue({
  el: '#app',
  render: h => h(App)
})
```

之后就可以在项目中使用 `D2-Crud` 了。

## CDN

externals: D2Crud

https://cdn.d2.pub/packages/@d2-projects/d2-crud@2.0.5/d2-crud.js


## 补丁修改
- 解决自带选择框 form-data-change 事件无法正确传递到父组件的问题
- 增加自定义查看按钮
- 增加查看功能，查看时元素默认disabled
- 自定义组件disabled 需要在props中增加  disabled: Boolean   组件属性写： :disabled="disabled"

- 使用：
``` js
<d2-crud v-bind:look-template="addTemplate"></d2-crud>
rowHandle: {
  look: {
    text: "查看",
    emit: "lookHandle"
  },
}
```



- 增加自定义按钮排序功能

- 使用：
``` js
rowHandle: {
  minWidth: "180px",
  look: {
    text: "查看",
    emit: "lookHandle",
    sort: 3
  },
  customs: [{
      text: '打卡记录',
      emit: 'showRecord',
      sort:2
    }],
  edit: {
    text: "编辑",
    emit: "editHandle",
    type: "warning ",
    sort: 1
  },

  }
```


- 增加纯文字查看
- 使用：
``` js
rowHandle: {
  lookNoEle: {
    text: "查看",
    emit: "lookHandle"
  },
}
```


- 自定义查看formatter
- 使用：
``` js
 mycom: {
    title: "选择框",
    value: "",
    component: {
      name: testCom,
      formatter(val) {
        return val === 1 ? "测试1" : "测试2";
      },
      props: {
        options: [
          { label: "测试1", value: 1 },
          { label: "测试2", value: 2 }
        ]
      }
    }
  },
```

- 自定义查看可自定义class
- 使用：
``` js
 roleName: {
    title: "角色名",
    value: "",
    class: "my_label",
    component: {
      placeholder: " 仅可输入英文大小写、数字"
    }
  },
```


-- 增加动态显示隐藏form表单
- 使用：
addTemplate值需要放在计算属性中
根据需要设置show的值
表单打开时如果是修改和查看也需要设置show值
``` js
 roleName: {
    title: "角色名",
    value: "",
    class: "my_label",
    component: {
      show: this.show === 1
      placeholder: " 仅可输入英文大小写、数字"
    }
  },
```

设置表单dialog的宽度
:add-width="400px"
:edit-width="400px"

=======
- 添加表单中自定义组件事件
-使用：
> 组件A
```
<template>
  <div>
    <el-button @click="up">up123</el-button>
  </div>
</template>

      up() {
        this.$emit("customEmit", 123);
      }

```
> 组件B
``` js
  methods:{
    handle(data){
      this.data=data
    }
  }
```
> 父组件
``` html
<d2-crud
@event:com-coma="handle">
</d2-crud>
```
``` js
 handle(data) {
    this.$refs.d2Crud.getRef("comb").handle(data);
  },
```


