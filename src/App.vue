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
      startSecond: '10',//开始时间，以秒为单位
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
