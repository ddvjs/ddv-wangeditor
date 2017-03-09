<template>
  <div id="editor" v-html="inputContent" @input="outputContent"></div>
</template>

<script>

export default{
  props: ['inputContent', 'uploadUrl'],
  data() {
    return {
      content: ''
    }
  },
  computed: {
  },
  mounted() {
    import('wangeditor')
    .then(wangeditor=>{
      this.createEditor(wangeditor)
    })
  },
  methods: {
    createEditor(WangEditor) {
      const self = this
      const editor = new WangEditor('editor')
      editor.config.menus = [
        'source', '|', 'bold', 'underline', 'italic', 'strikethrough', 'eraser', 'forecolor', 'bgcolor', '|', 'quote', 'fontfamily', 'fontsize', 'head', 'unorderlist', 'orderlist', 'alignleft', 'aligncenter', 'alignright',
        '|', 'link', 'unlink', 'table', 'img', 'video', 'insertcode', '|', 'undo', 'redo', 'fullscreen'
      ]
      editor.config.uploadImgUrl = this.uploadUrl
      editor.onchange = function() {
        self.formatContent(this.$txt.html())
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

<style lang="css" scoped>
  .wangEditor-container{
    border-radius: 2px;
    overflow: hidden;
    border: 1px solid #CCC;
  }
</style>
