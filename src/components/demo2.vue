<template>
  <div id="app">
    <!-- :klineParams="klineParams" :klineData="klineData" 绑定下面data数据 用于自定制数据传输到vue-kline, ref="callMethods"绑定一个DOM事件 用于调用接口  --->
    <Vue-kline :klineParams="klineParams" :klineData="klineData" ref="callMethods" @refreshKlineData="refreshKlineData"></Vue-kline>
    <router-link to="/">Go to Demo1</router-link>
  </div>
</template>
<script>
import VueKline from "../kline/kline";
import data from "@/assets/data";
export default {
  name: "Demo2",
  components: {
    VueKline
  },
  data() {
    return {
      klineParams: {
        width: 800,
        height: 500,
        theme: "dark",
        language: "zh-cn",
        ranges: ["1w", "1d", "1h", "30m", "15m", "5m", "1m", "line"],
        symbol: "BTC",
        symbolName: "BTC/USD",
        intervalTime: 5000,
        depthWidth: 50,
        count: 1,
      },
      klineData: {}
    };
  },
  mounted(){
    this.refreshKlineData(900000);// 进入页面时执行,默认聚合时间900000毫秒(15分钟)
  },
  methods:{
    requestData(){              //方法名任意取
       /*测试用的  请求服务器请用下面的*/
      this.klineData = data;
      this.$refs.callMethods.kline.chartMgr.getChart().updateDataAndDisplay(data.data.lines);


      // this.$axios.request({
      //   url: "xxxxx",             //请求地址
      //   method: "POST"
      // }).then(ret => {
      //   this.klineData = ret.data;      // 把返回数据赋值到上面的 klineData,
      //   this.$refs.callMethods.kline.chartMgr.getChart().updateDataAndDisplay(ret.data.data.lines); //强制更改缓存中的lines值,防止显示不同步
      // });
    },
    refreshKlineData(option){  //你点击页面上的周期会触发这个方法
        if (option===900000){   //如果时间等于15分钟
          this.requestData();
        }else if(option===300000){//如果5分钟
          console.log("5分钟"+option)
        }else{
          console.log("其他时间"+option) //其他时间
        }
    },
  }
};
</script>
