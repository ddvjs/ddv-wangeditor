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
import { ddvWangeditor } from 'vue-video-player'
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
  	:upload-url="uploadURL"
  	v-model="outputContent"></ddv-wangeditor>
</template>

  export default {
    //输入内容到编辑器
    inputContent: 'asdsad',
    //从编辑器输出的内容
    outputContent: 'asdsad',
    //设置图片上传API网址
    uploadURL: '/11111'
  }

```

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/es5-shim/3.4.0/es5-shim.min.js"></script>
```
