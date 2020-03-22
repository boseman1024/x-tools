<template>
  <div class="home">
    <Header></Header>
    <zi-tabs>
     <zi-tabs-item :label="'编码库'" :value="'code'">
        <CodeTrans></CodeTrans>
      </zi-tabs-item>
      <zi-tabs-item :label="'颜料板'" :value="'color'">
        <Color></Color>
      </zi-tabs-item>
      <zi-tabs-item :label="'JSON编辑器'" :value="'json'">
        <JsonEditor></JsonEditor>
      </zi-tabs-item>
    </zi-tabs>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import CodeTrans from '@/components/CodeTrans.vue';
import Color from '@/components/Color.vue';
import JsonEditor from '@/components/JsonEditor.vue';
export default {
  name: 'Home',
  components: {
    Header,CodeTrans,Color,JsonEditor
  }
}
</script>
