<template>
  <div class="JsonEditor">
    <div id="jsoneditor" style="width: 100%; height: 600px;"></div>
  </div>
</template>

<script>
import JSONEditor from 'jsoneditor';
import 'jsoneditor/dist/jsoneditor.min.css';
export default {
  name: 'JsonEditor',
  components: {
    
  },
  data(){
    return {
      data:{
        label:'JSON编辑器',
        desc:'输入内容'
      }
    }
  },
  methods:{
    
  },
  mounted(){
    const container = document.getElementById("jsoneditor");
    const options = {
      mode: 'tree',
      modes: ['code', 'form', 'text', 'tree', 'view', 'preview'],
      language: 'zh-CN',
    };
    const editor = new JSONEditor(container, options);
    editor.set(this.data);
  }
}
</script>
<style scoped lang="less">

</style>

