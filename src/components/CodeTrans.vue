<template>
  <div class="CodeTrans">
    <zi-card>
        <zi-spacer :y="1"></zi-spacer>
        <zi-radio-group v-model="type" class="types">
          <zi-radio v-for="i in typeOpt" :key="i.value" :label="i.value">{{i.label}}</zi-radio>
        </zi-radio-group>
        <zi-spacer :y="1"></zi-spacer>
        <zi-textarea v-model="input" :placeholder="'请输入内容'" :type="inputStatus"></zi-textarea>
         <zi-spacer :y="1"></zi-spacer>
        <zi-input v-model="key" :placeholder="'请输入密钥'" prefix-label="密钥" v-if="needKey()"></zi-input>
        <zi-spacer :y="1"></zi-spacer>
        <zi-row>
          <zi-col>
            <zi-button ghost type="primary" size="small" @click="encrypt">加密</zi-button>
          </zi-col>
          <zi-spacer :x="1"></zi-spacer>
          <zi-col>
            <zi-button ghost type="primary" size="small" @click="decrypt" :disabled="canDecrypt()">解密</zi-button>
          </zi-col>
        </zi-row>
        <zi-more :text="'结果'" :loading="loading"></zi-more>
        <zi-textarea v-model="result" :placeholder="'结果'" readonly></zi-textarea>
      
    </zi-card>
  </div>
</template>

<script>
import CryptoJS from 'crypto-js';
export default {
  name: 'CodeTrans',
  data(){
    return {
      type:0,
      loading:false,
      typeOpt:[{
        label:'Base64',
        value:0
      },{
        label:'MD5',
        value:1
      },{
        label:'SHA1',
        value:2
      },{
        label:'SHA224',
        value:3
      },{
        label:'SHA256',
        value:4
      },{
        label:'SHA384',
        value:5
      },{
        label:'SHA512',
        value:6
      },{
        label:'RIPEMD160',
        value:7
      },{
        label:'HmacMD5',
        value:8
      },{
        label:'HmacSHA1',
        value:9
      },{
        label:'HmacSHA224',
        value:10
      },{
        label:'HmacSHA256',
        value:11
      },{
        label:'HmacSHA384',
        value:12
      },{
        label:'HmacSHA512',
        value:13
      },{
        label:'HmacRIPEMD160',
        value:14
      },{
        label:'AES',
        value:15
      },{
        label:'DES',
        value:16
      },{
        label:'TripleDES',
        value:17
      },{
        label:'RC4',
        value:18
      },{
        label:'RABBIT',
        value:19
      }],
      inputStatus:'primary',
      input:'',
      key:'',
      result:''
    }
  },
  methods:{
    encrypt(){
      this.loading = true;
      try {
        if(this.type==0){
          this.result = CryptoJS.enc.Utf8.parse(this.input).toString(CryptoJS.enc.Base64);
        }
        if(this.type==1){
          this.result = CryptoJS.MD5(this.input).toString();
        }
        if(this.type==2){
          this.result = CryptoJS.SHA1(this.input).toString();
        }
        if(this.type==3){
          this.result = CryptoJS.SHA224(this.input).toString();
        }
        if(this.type==4){
          this.result = CryptoJS.SHA256(this.input).toString();
        }
        if(this.type==5){
          this.result = CryptoJS.SHA384(this.input).toString();
        }
        if(this.type==6){
          this.result = CryptoJS.SHA512(this.input).toString();
        }
        if(this.type==7){
          this.result = CryptoJS.RIPEMD160(this.input).toString();
        }
        if(this.type==8){
          this.result = CryptoJS.HmacMD5(this.input,this.key).toString();
        }
        if(this.type==9){
          this.result = CryptoJS.HmacSHA1(this.input,this.key).toString();
        }
        if(this.type==10){
          this.result = CryptoJS.HmacSHA224(this.input,this.key).toString();
        }
        if(this.type==11){
          this.result = CryptoJS.HmacSHA256(this.input,this.key).toString();
        }
        if(this.type==12){
          this.result = CryptoJS.HmacSHA384(this.input,this.key).toString();
        }
        if(this.type==13){
          this.result = CryptoJS.HmacSHA512(this.input,this.key).toString();
        }
        if(this.type==14){
          this.result = CryptoJS.HmacRIPEMD160(this.input,this.key).toString();
        }
        if(this.type==15){
          this.result = CryptoJS.AES.encrypt(this.input,this.key).toString();
        }
        if(this.type==16){
          this.result = CryptoJS.DES.encrypt(this.input,this.key).toString();
        }
        if(this.type==17){
          this.result = CryptoJS.TripleDES.encrypt(this.input,this.key).toString();
        }
        if(this.type==18){
          this.result = CryptoJS.RC4.encrypt(this.input,this.key).toString();
        }
        if(this.type==19){
          this.result = CryptoJS.Rabbit.encrypt(this.input,this.key).toString();
        }
        this.inputStatus = 'primary';
      }catch(err){
           this.inputStatus = 'danger';
           this.ToastErr();
      }finally{
        this.loading = false;
      }
    },
    decrypt(){
      this.loading = true;
      try {
        if(this.type==0){
          this.result = CryptoJS.enc.Base64.parse(this.input).toString(CryptoJS.enc.Utf8);
        }
        if(this.type==15){
          this.result = CryptoJS.AES.decrypt(this.input,this.key).toString(CryptoJS.enc.Utf8);
        }
        if(this.type==16){
          this.result = CryptoJS.DES.decrypt(this.input,this.key).toString(CryptoJS.enc.Utf8);
        }
        if(this.type==17){
          this.result = CryptoJS.TripleDES.decrypt(this.input,this.key).toString(CryptoJS.enc.Utf8);
        }
        if(this.type==18){
          this.result = CryptoJS.RC4.decrypt(this.input,this.key).toString(CryptoJS.enc.Utf8);
        }
        if(this.type==19){
          this.result = CryptoJS.Rabbit.decrypt(this.input,this.key).toString(CryptoJS.enc.Utf8);
        }
        this.inputStatus = 'primary';
      }catch(err){
           this.inputStatus = 'danger';
           this.ToastErr();
      }finally{
        this.loading = false;
      }
    },
    canDecrypt(){
      return this.type==1||this.type==2||this.type==3||this.type==4||this.type==5||this.type==6||this.type==7||this.type==8||this.type==9||this.type==10||this.type==11||this.type==12||this.type==13||this.type==14;
    },
    needKey(){
      return this.type==8||this.type==9||this.type==10||this.type==11||this.type==12||this.type==13||this.type==14||this.type==15||this.type==16||this.type==17||this.type==18||this.type==19;
    },
    ToastErr(){
      const instance = this.$Toast.show({
        type: 'danger',
        action: '关闭',
        text: '无法解析',
        handler: () => instance.close(),
      })
    }
  }
}
</script>
<style scoped>
  .types{
    text-align: left;
  }
</style>