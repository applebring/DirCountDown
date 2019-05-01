# 自定义倒计时组件

## component install 组件引入
```
npm/cnpm install --save-dev dircountdown
```
## file of vue reference vue文件引入
```
import CountDown from 'dircountdown'
components:{CountDown}
```
## html reference       html引入
 `<dir-clock :start="startSecond" end="0" style="color:#000;" v-on:endcallback="endFn" :autoshow='false' splitsymbol="时-分-秒" :autostart="false" ref="countdown"></dir-clock>`
## props 属性
Props属性|describe属性描述
-|-|
start| 开始时间(以秒为单位如一分钟则为3600) starttime（in seconds,like a minute is 3600）
end|结束时间 endTime                                                                  
endcallback|当时间为0时的回调函数   callback function when time ends with zero                 
autoshow|当小时为0时或者小时分钟都为0时，是否隐藏例如00：00：30则显示为30 when hour or minute is zero,they will be hide,like 00:00:30 is 30                
splitsymbol|时分秒分割单位 (时-分-秒||：-：-：)       symbol to split time                      
autostart|是否一进入就进行倒计时     whether to start when enter the page                    

## Demo
```
app.vue
<template>
  <div id="app">
    <count-down :start="startSecond" end="0" style="color:#000;" v-on:endcallback="endFn" :autoshow='false' splitsymbol="时-分-秒" :autostart="false" ref="countdown"></count-down>
    <button @click="startCount">开始计时</button>
  </div>
</template>

<script>
import CountDown from 'dircountdown'
export default {
  name: 'App',
  data(){
    return{
      startSecond: '10',
    }
  },
  methods:{
    endFn(){
      alert("时间到!");
    },
    startCount(){
      this.$refs.countdown.countTime();
    }
  },
  components:{CountDown}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```


