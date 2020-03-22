<template>
  <div class="Color">
    <zi-spacer :y="1"></zi-spacer>
    <zi-radio-group v-model="column">
        <zi-radio v-for="i in columnOpt" :key="i.value" :label="i.value">{{i.label}}</zi-radio>
    </zi-radio-group>
    <zi-spacer :y="1"></zi-spacer>
    <div v-if="column==0">
      <zi-card style="height:500px;" :style="'background:'+color.hex">
          <zi-row :justify="'space-around'" :align="'middle'">
            <zi-col>
              <h1 class="color-label" @click="copyColor(color)" :style="'color:rgb('+(255-color.rgba.r)/2+','+(255-color.rgba.g)/2+','+(255-color.rgba.b)/2+')'">{{color.hex}}</h1>
              <sketch-picker v-model="color" class="picker"/>
            </zi-col>
          </zi-row>
      </zi-card>
    </div>
    <div v-if="column==1">
          <zi-fieldset>
            <div :style="transColor(0)">
              <zi-row :justify="'space-around'" :align="'middle'" style="height:450px;" v-for="(i,index) in colorTrans" :key="index">
                <zi-col>
                  <span class="color-label" @click="copyColor(i)" :style="'color:rgb('+(255-i.rgba.r)/2+','+(255-i.rgba.g)/2+','+(255-i.rgba.b)/2+')'">{{i.hex}}</span>
                  <sketch-picker v-model="colorTrans[index]" class="picker"/>
                </zi-col>
              </zi-row>
            </div>
            <template slot="footer">
              <div :style="transColor(1)" class="trans-color-block"></div>
              <div>
                <zi-button  @click="addTransColor()" type="primary" auto ghost size="small" style="margin-right: 10px;">添加</zi-button>
                <zi-button  @click="delTransColor()" type="danger" auto size="small">删除</zi-button>
              </div>
            </template>
           
          </zi-fieldset>
    </div>
    <div v-if="column==2">
      <zi-card>
          <zi-description :title="'中国传统色彩'" :content="''"></zi-description>
          <div class="flex">
              <div class="color-block" v-for="(i,index) in chineseTraditionalColor" :key="index" :style="'background:'+i.hex" @click="copyColor(i)">
                <div>{{i.hex}}</div>
                <div>{{i.name}}</div>
              </div>
          </div>
      </zi-card>
    </div>
  </div>
</template>

<script>
import { Sketch } from 'vue-color';
import chineseTraditionalColor from '@/assets/chineseTraditionalColor'
export default {
  name: 'Color',
  components: {
    'sketch-picker': Sketch
  },
  data(){
    return {
      chineseTraditionalColor,
      columnOpt:[{
        label:'取色板',
        value:0
      },{
        label:'渐变色',
        value:1
      },{
        label:'颜料堆',
        value:2
      }],
      column:0,
      color:{
        hex:'#56CCFF',
        rgba:{
          r:86,
          g:204,
          b:255,
          a:1
        }
      },
      colorTrans:[{
        hex:'#9cecfb',
        rgba:{
          r:156,
          g:236,
          b:251,
          a:1
        }
      },{
        hex:'#0052d4',
        rgba:{
          r:0,
          g:82,
          b:212,
          a:1
        }
      }]
    }
  },
  methods:{
    transColor(type){
      let colors = [];
      for(let i of this.colorTrans){
        colors.push(i.hex);
      }
      let colorsStr = ''+colors.join(',');
      if(type==1){
        colorsStr = 'to right,'+colorsStr;
      }
      return 'background:linear-gradient('+colorsStr+');';
    },
    addTransColor(){
      if(this.colorTrans.length>5){
        const instance = this.$Toast.show({
          type: 'danger',
          action: '关闭',
          text: '太多了',
          handler: () => instance.close(),
        })
        return;
      }
      this.colorTrans.push({
        hex:'#ffffff',
        rgba:{
          r:255,
          g:255,
          b:255,
          a:1
        }
      });
      const instance = this.$Toast.show({
        type:'success',
        action: '关闭',
        text: '+1',
        handler: () => instance.close(),
      });
    },
    delTransColor(){
      if(this.colorTrans.length==2){
        const instance = this.$Toast.show({
          type: 'danger',
          action: '关闭',
          text: '不能再少了',
          handler: () => instance.close(),
        });
        return;
      }
      this.colorTrans.pop();
      const instance = this.$Toast.show({
        type:'success',
        action: '关闭',
        text: '-1',
        handler: () => instance.close(),
      });
    },
    copyColor(color){
      const temp = document.createElement("input"); 
      temp.setAttribute("value", color.hex); 
      document.body.appendChild(temp); 
      temp.select();
      document.execCommand("copy"); 
      document.body.removeChild(temp);
      const instance = this.$Toast.show({
        type:'success',
        action: '关闭',
        text: '复制成功：'+(color.name?color.name:'')+' '+color.hex,
        handler: () => instance.close(),
      });
    }
  }
}
</script>
<style scoped lang="less">
.Color{
  padding-bottom:20px;
  .picker{
    margin:0 auto;
  }
  .color-label{
    text-align:center;
    text-shadow: #e3e3e3 5px 0 4px, #e3e3e3 0 5px 4px, #e3e3e3 -1px 0 3px, #e3e3e3 0 -1px 3px;
    font-size: 3rem;
    letter-spacing: -.066875rem;
    line-height: 1.5;
    font-weight: 700;
    cursor:pointer;
  }
  .trans-color-block{
    width:50%;
    height:30px;
  }
  .flex{
    display:flex;
    flex-wrap:wrap;
    justify-content: space-around;
    align-items: center;
  }
  .color-block{
    width:200px;
    text-align:center;
    line-height:30px;
    padding:10px 0;
    border-radius:7px;
    margin:10px 0;
    cursor:pointer;
  }
}

</style>

