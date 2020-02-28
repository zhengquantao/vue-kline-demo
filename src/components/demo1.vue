<template>
  <div id="app">
    <Vue-kline :klineParams="klineParams" :klineData="klineData"></Vue-kline>
    <router-link to="demo2">Go to Demo2</router-link>
  </div>
</template>
<script>
import VueKline from "vue-kline";
import data from "@/assets/data";

export default {
  name: "Demo1",
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
      klineData: data,
    };
  }
};
</script>
