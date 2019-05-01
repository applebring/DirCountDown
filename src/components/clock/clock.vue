<template>
  <div style="font-size:20px;">
    <i class="iconfont icon-clock"></i>
    <template v-if="showhour&&!showmin">
      <span>{{minute}}{{splitsymbol.split("-")[1]?splitsymbol.split("-")[1]:''}}{{second}}{{splitsymbol.split("-")[2]?splitsymbol.split("-")[2]:''}}</span>
    </template>
    <template v-if="showhour&&showmin">
      <span>{{hour}}{{splitsymbol.split("-")[0]?splitsymbol.split("-")[0]:''}}{{minute}}{{splitsymbol.split("-")[1]?splitsymbol.split("-")[1]:''}}{{second}}{{splitsymbol.split("-")[2]?splitsymbol.split("-")[2]:''}}</span>
    </template>
    <template v-if="!showhour&&!showmin">
      <span>{{second}}{{splitsymbol.split("-")[2]?splitsymbol.split("-")[2]:''}}</span>
    </template>
  </div>
</template>
<script>
export default {
  data() {
    return {
      timer: null,
      gettime: 0, //获取传入的时间
      hour: 0, //小时
      minute: 0, //分钟
      second: 0, //秒
      showhour: true, //当小时为0是否继续展示
      showmin: true
    };
  },
  props: {
    start: {
      //开始时间
      type: String,
      default: 0 //以秒来算
    },
    end: {
      //结束时间
      type: String,
      default: 0
    },
    autoshow: {
      //当为00时，不显示
      type: Boolean,
      default: false
    },
    EndCallBack: {
      //时间为0时的回调函数
      type: Function
    },
    splitsymbol: {
      //分割符
      type: String,
      default: ":-:-:"
    },
    autostart: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    //时间为0时候触发的函数
    timeToEnd() {
      this.$emit("endcallback");
    },
    countTime() {
      let $self = this;
      this.gettime = this.start;
      this.timer = setInterval(() => {
        if(this.gettime!==0){ this.gettime--;}
        if (this.gettime == 0) {
          let $self = this;
          this.timeToEnd();
          clearInterval(this.timer);
        }
        this.currentTime(this.gettime);
       
      }, 1000);
    },
    currentTime(time){
      let h = Math.floor(time / 3600); //1h = 3600s;
        let m = Math.floor((time / 60) % 60); // 1min = 60s;
        let s = Math.floor(time % 60);
        if (h < 10 || h == 0) {
          h = "0" + h;
        }
        if (m < 10 || m == 0) {
          m = "0" + m;
        }
        if (s < 10 || s == 0) {
          s = "0" + s;
        }
        if (this.autoshow && h == "00") {
          this.showhour = false;
        }
        if (this.autoshow && h == "00" && m == "00") {
          this.showhour = false;
          this.showmin = false;
        }
        this.hour = h;
        this.minute = m;
        this.second = s;
    }
  },
  mounted() {
    if (this.start > 216000) {
      alert("设置起始时间不可超过3600*60秒");
      return;
    }
    this.currentTime(this.start);
    if (this.autostart) {
      this.countTime();
    }
  }
};
</script>