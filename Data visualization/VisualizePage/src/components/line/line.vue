<!-- 层叠柱状图 -->
<style lang="stylus" scoped>
.line {
  height: 1000px;
  background: url('../../assets/bg.jpg') no-repeat;
  background-size: 100% 100%;

  .main {
    width: 100%;
    height: calc(100% - 100px);
    margin-top: -15px;
  }
}
</style>

<template>
  <div class="line">
    <v-header :name="name" :legendArr="legendArr" :myChart="myChart"></v-header>
    <!-- <v-filter :myChart="myChart" v-if="myChart._dom"></v-filter> -->
    <div class="main" style="margin-top:20px"></div>
  </div>
</template>

<script>
import echarts from "echarts";
import header from "components/header/header";
import filter from "components/filter/filter";
import wordcloud from "vue-wordcloud";

export default {
  data() {
    return {
      legendArr: [],
      color: this.$store.state.color,
      myChart: {},
      name: "Series-Line"
    };
  },
  components: {
    "v-header": header,
    "v-filter": filter
  },
  mounted() {
    this.myChart = echarts.init(document.querySelector('.line .main'));
    this.myChart.setOption({
      title: {
        show: false
      },
      tooltip: {
        trigger: 'axis'
      },
      legend: {
        show: false
      },
      toolbox: {
        show: false
      },
      color: this.color,
      calculable: true,
      xAxis: [
        {
          name: 'state',
          type: 'category',
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          nameTextStyle: {
            color: 'rgba(255, 255, 255, 0.69)'
          },
          axisLabel: {
            textStyle: {
              color: 'white'
            }
          },
          data: ['CA', 'TX', 'FL', 'NY', 'PA', 'IL', 'Ohio']
        }
      ],
      yAxis: [{
        axisLine: {
          show: false
        },
        nameLocation: 'end',
        nameGap: 20,
        nameRotate: 0,
        axisTick: {
          show: false
        },
        splitLine: {
          lineStyle: {
            color: ['rgba(230, 230, 230, 0.2)']
          }
        },
        axisLabel: {
          textStyle: {
            color: 'white',
            fontSize: 14
          }
        },
        name: 'number',
        type: 'value',
        nameTextStyle: {
          color: 'rgba(255, 255, 255, 0.69)'
        }
      }],
      series: [{
        name: 'Positive',
        type: 'line',
        data: [120, 132, 101, 134, 90, 230, 210]
      }, {
        name: 'Neutral',
        type: 'line',
        data: [220, 182, 191, 234, 290, 330, 310]
      }, {
        name: 'Negative',
        type: 'line',
        data: [150, 232, 201, 154, 190, 330, 410]
      }, {
        name: 'Total',
        type: 'line',
        data: [320, 332, 301, 334, 390, 330, 320]
      }]
    });
    this._init()
  }
};
</script>
