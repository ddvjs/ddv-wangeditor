<template>
  <div v-html="inputContent" @input="outputContent" ref="editor"></div>
</template>

<script>
const uploadInit = require('../lib/uploadInit.js');
export default{
  props: {
    inputContent:String,
    menus:Array,
    httpRequest:{
      type:Function,
      default:null
    }
  },
  data() {
    return {
      content: ''
    }
  },
  mounted() {
    var startTime = new Date()
    var timeer = setInterval(()=>{
      if ((this.$refs.editor && this.$refs.editor.clientWidth) || new Date() - startTime>=3000) {
        clearInterval(timeer)
        import('wangeditor').then(WangEditor=>this.createEditor(WangEditor))
      }
    },100)
  },
  methods: {
    createEditor(WangEditor) {
      const self = this
      const editor = new WangEditor(this.$refs.editor)

      if(this.menus instanceof Array && this.menus.length !== 0){
        editor.config.menus = this.menus
      }else{
        editor.config.menus = [
          'source', '|', 'bold', 'underline', 'italic', 'strikethrough', 'eraser', 'forecolor', 'bgcolor', '|', 'quote', 'fontfamily', 'fontsize', 'head', 'unorderlist', 'orderlist', 'alignleft', 'aligncenter', 'alignright',
          '|', 'link', 'unlink', 'table', 'img', 'video', 'insertcode', '|', 'undo', 'redo', 'fullscreen'
        ]
      }
      // editor.config.uploadImgUrl = this.uploadUrl
      editor.onchange = function() {
        self.formatContent(this.$txt.html())
      }
      if (this.httpRequest&&typeof this.httpRequest === 'function') {
        editor.config.customUpload = true;  // 设置自定义上传的开关
        editor.config.customUploadInit = uploadInit(this.httpRequest);  // 配置自定义上传初始化事件，uploadInit方法在上面定义了
      }
      editor.create()
    },
    formatContent(content) {
      this.content = content
      this.outputContent()
    },
    outputContent() {
      this.$emit('input', this.content)
    }
  }
}
</script>
<style lang='css' src="wangeditor/dist/css/wangEditor.css"></style>

<style lang="css" scoped>
  .wangEditor-container{
    border-radius: 2px;
    overflow: hidden;
    border: 1px solid #CCC;
  }
</style>
