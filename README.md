# ddv-wangeditor
>这是一个基于[wangEditor](https://github.com/wangfupeng1988/wangEditor)的富文本编辑器
>支持[vue](https://github.com/vuejs/vue)2.0版本
## 安装

**npm:**

```shell
$ npm install ddv-wangeditor
```

**引入:**

```javascript
// import with ES6
import Vue from 'vue'
import ddvWangeditor from 'ddv-wangeditor'

// use
Vue.use(ddvWangeditor)

// or use with component(ES6)
import Vue from 'vue'
import { ddvWangeditor } from 'ddv-wangeditor'
// use
export default {
  components: {
    ddvWangeditor
  }
}

//使用
<template>
  <ddv-wangeditor
  	:input-content="inputContent"
    :menus="menus"
    :http-request="httpRequest"
  	v-model="outputContent"></ddv-wangeditor>
</template>  

  export default {
    data () {
      //输入内容到编辑器
      inputContent: 'asdsad',
      //从编辑器输出的内容
      outputContent: 'asdsad',
      //编辑器工具栏配置,可选，默认全部
      menus:[]
    },
    methods: {
      //自定义图片上传模块
      httpRequest(options){

      }
    }
  }

```
