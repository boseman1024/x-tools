<template>
  <div class="Header">
    <zi-row :justify="'space-between'" :align="'middle'">
      <zi-col :span="19"><h2>{{name}}</h2></zi-col>
      <zi-col :span="5"><zi-link :href="''" color>Github</zi-link></zi-col>
    </zi-row>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return {
      name:'Axisx Tools'
    }
  }
}
</script>
<style lang="less">
.Header{
  text-align:left;
}
</style>

