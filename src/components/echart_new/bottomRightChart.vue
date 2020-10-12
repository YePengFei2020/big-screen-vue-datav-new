<template>
  <div>
    <div id="bottomRightChart" style="width:11.125rem; height: 5.88rem;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";

export default {
  data() {
    return {
      chart: null,
      datas: []
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
    this.charData();
  },
  methods: {
    charData() {
      this.datas =  [99,80,65,32,30,28,28]
      setInterval(() => {
        for(let i=0;i<this.datas.length;i++){
          this.datas[i] = this.RandomNum(1,500)
        }
        // console.log(this.datas)
        this.draw()
      }, 3000);
    },
    RandomNum(Min, Max) {
      var Range = Max - Min;
      var Rand = Math.random();
      if(Math.round(Rand * Range)==0){      
        return Min + 1;
      }
      var num = Min + Math.round(Rand * Range);
      return num;
    },
    draw() {
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(document.getElementById("bottomRightChart"));
      //  ----------------------------------------------------------------
        let option = {
        legend: {
          formatter: function (params) {
            var tmp = ''
            var res = ''
            tmp = params.split('\n')
            res = '' + params
            for (var i in tmp) {
              res = res.replace(tmp[i], '')
            }
            return res + params
          },
          x: 145,
          y: 2,
          itemWidth: 15, // 设置宽度
          itemHeight: 6 // 设置高度
        },
        xAxis: [
          {
            type: 'category',
            data: ['2015年', '2016年', '2017年', '2018年', '2019年'],
            axisPointer: {
              type: 'shadow'
            },
            axisLabel: { // X轴线 标签修改
              textStyle: {
                color: '#5A5A5A' // 坐标值的具体的颜色
              }
            },
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            }
          }
        ],
        yAxis: [
          {
            type: 'value',
            // name: '水量',
            min: 0,
            max: 150,
            axisLabel: { // X轴线 标签修改
              textStyle: {
                color: '#5A5A5A' // 坐标值得具体的颜色
              }
            },
            axisLine: {
              show: false
            },
            axisTick: {
              show: false
            }
          }
        ],
        grid: { // 设置canvas内部表格的内距
          x: 40,
          // y: 50,
          x2: 40,
          // y2: 60,
          borderWidth: 10
        },
        series: [
          {
            name: '本期',
            type: 'line',
            data: [20, 49, 70, 22, 26],
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 2,
                color: '#E6350D'
              }
            }
          },
          {
            name: '同期',
            type: 'line',
            data: [26, 59, 90, 24, 27],
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 2,
                color: '#FFAC4C'
              }
            }
          }
        ]
      }
      this.chart.setOption(option);
    }
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
</style>