<template xmlns:v-bind="http://www.w3.org/1999/xhtml" xmlns:v-on="http://www.w3.org/1999/xhtml">
  <div id="app">
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button>
    <br>
    千米 : <input type = "text" v-model = "kilometers">
    米 : <input type = "text" v-model = "meters">

    <br>

    <div v-bind:class="{ active: isActive }"></div>
    <br>
    <button v-on:click="greet">Greet</button>
    <br>

    <button v-on:click="say('hi')">Say hi</button>
    <button v-on:click="say('what')">Say what</button>
    <br>

    <p>input 元素：</p>
    <input v-model="message" placeholder="编辑我……">
    <p>消息是: {{ message }}</p>

    <p>textarea 元素：</p>
    <p style="white-space: pre">{{ message2 }}</p>
    <textarea v-model="message2" placeholder="多行文本输入……"></textarea>

    <br>
    <p>单个复选框：</p>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>

    <p>多个复选框：</p>
    <input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
    <label for="runoob">Runoob</label>
    <input type="checkbox" id="google" value="Google" v-model="checkedNames">
    <label for="google">Google</label>
    <input type="checkbox" id="taobao" value="Taobao" v-model="checkedNames">
    <label for="taobao">taobao</label>
    <br>
    <span>选择的值为: {{ checkedNames }}</span>


    <br>
    <input type="radio" id="runoob1" value="Runoob" v-model="picked">
    <label for="runoob1">Runoob</label>
    <br>
    <input type="radio" id="google1" value="Google" v-model="picked">
    <label for="google1">Google</label>
    <br>
    <span>选中值为: {{ picked }}</span>
    <br>

    <select v-model="selected" name="fruit">
      <option value="">选择一个网站</option>
      <option value="www.runoob.com">Runoob</option>
      <option value="www.google.com">Google</option>
    </select>

    <div id="output">
      选择的网站是: {{selected}}
    </div>

    <parent></parent>
    <br>
    <button v-on:click="ajaxTest">ajaxTest</button>

    <br>
    <button v-on:click="ajaxTest1">ajaxTest1</button>

  </div>
</template>

<script>

import parent from './components/parent'

export default {
  name: 'App',
  components: {
    parent
  },
  data (){
      return{
        counter:'1',
        kilometers:0,
        meters:0,
        isActive:true,
        message:'Runoob',
        message2:'11111111',
        checked:false,
        checkedNames:[],
        picked:'Runoob',
        selected:''
      }
  },
  watch:{
    counter:function (nval,oval) {
      console.log('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
    },
    kilometers:function (val) {
      this.kilometers = val;
      this.meters = val*1000;
    },
    meters:function (val) {
      this.kilometers = val/1000;
      this.meters = val;
    }

  },
  methods:{
    greet:function (event) {
      console.log(111111111);
    },
    say:function (message) {
      console.log(message);
    },
    ajaxTest:function () {
      this.$api.post('/ssm/user/queryById', {"age":10,"userName":"javen"}, response => {
        if (response.status >= 200 && response.status < 300) {
          console.log(response.data[0].userName);
        } else {
          console.log(response.message);
        }
      });
    },
    ajaxTest1:function () {
      this.$api.post('/ssm/user/query', {}, response => {
        if (response.status >= 200 && response.status < 300) {
          console.log(response.data.userName);
        } else {
          console.log(response.message);
        }
      });
    }

  }

}

</script>

<style>
  .active {
    width: 100px;
    height: 100px;
    background: green;
  }
</style>
