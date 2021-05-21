<!-- 散点图 -->
<style lang="stylus" scoped>
.point {
  background: url('../../assets/bg.jpg') no-repeat;
  background-size: 100% 100%;

  .main {
    height: calc(100% - 120px);
    width: 100%;
    transition: all 0.5s linear;
  }
}

.filter {
  position: relative;
  display: flex;
  padding: 10px 0 0 28px;
  font-size: 12px;
  line-height: 11px;
  color: white;
  z-index: 9999;

  .myCalendar {
    left: auto !important;
  }

  input {
    background: transparent;
    border: none;
    color: white;
  }

  .timeText {
    opacity: 0.69;
    padding-right: 7px;
  }

  .startTime {
    display: inline-block;
  }

  .endTime {
    display: inline-block;
    padding-left: 42px;
  }

  .el-date-editor {
    width: 55%;
  }

  .products {
    position: absolute;
    display: inline-block;
    right: 15px;

    .all {
      display: inline-block;
      margin-right: 18px;

      .v-checkbox {
        position: relative;
        top: 2px;
        left: -3px;
      }
    }

    .pro {
      float: right;
      padding: 2px 25px 2px 2px;

      .arrow {
        position: absolute;
        width: 6px;
        height: 6px;
        margin-left: 10px;
        border-left: 2px solid white;
        border-bottom: 2px solid white;
        transform: rotate(-45deg);
      }
    }
  }

  .pro_list {
    position: absolute;
    right: 22px;
    width: 102px;
    text-align: left;
    background: #1e3642;
    font-size: 14px;
    margin-top: 22px;
    /* max-height 180px */
    overflow: hidden;
    z-index: 9;

    li {
      height: 36px;
      line-height: 36px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);

      &:last-child {
        border: none;
      }

      .v-checkbox {
        left: 8px;
      }

      .name {
        position: absolute;
        display: inline-block;
        right: 8px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 70px;
      }
    }
  }
}
</style>

<template lang="html">

<div class="point">

  
  <v-header :name="name" :legendArr="legendArr" :myChart="myChart">
  </v-header>
      <el-radio-group class="filter" fill="#9de089" size="medium" v-model="radio1" style="float:right;padding-right:10px;margin-top:-50px" @change="changeOption">
      <el-radio-button label="Positive"></el-radio-button>
      <el-radio-button label="Negative"></el-radio-button>
    </el-radio-group>
  <!-- <v-filter :myChart="myChart" v-if="myChart._dom"></v-filter> -->
  <div class="main"></div>
</div>
</template>

<script>
import axios from "axios";
import echarts from "echarts";
import usa from "echarts/map/js/usa";
import header from "components/header/header";
import filter from "components/filter/filter";
export default {
  created() {
    this._getCityData();
  },
  data() {
    return {
      legendArr: [],
      color: this.$store.state.color,
      myChart: {},
      geoCoordMap: {},
      name: "SentimentAnalysis",
      radio1: "Positive",
      options: {},
      option_data: [
        {
          name: "Alaska",
          value: 0
        },
        {
          name: "Alabama",
          value: 93
        },
        {
          name: "Arkansas",
          value: 8
        },
        {
          name: "Arizona",
          value: 0
        },
        {
          name: "California",
          value: 202
        },
        {
          name: "Colorado",
          value: 36
        },
        {
          name: "Connecticut",
          value: 36
        },
        {
          name: "Delaware",
          value: 297
        },
        {
          name: "Florida",
          value: 40
        },
        {
          name: "Georgia",
          value: 21
        },
        {
          name: "Hawaii",
          value: 28
        },
        {
          name: "Idaho",
          value: 3
        },
        {
          name: "Illinois",
          value: 74
        },
        {
          name: "Indiana",
          value: 37
        },
        {
          name: "Iowa",
          value: 4
        },
        {
          name: "Kansas",
          value: 32
        },
        {
          name: "Kentucky",
          value: 31
        },
        {
          name: "Louisiana",
          value: 25
        },
        {
          name: "Massachusetts",
          value: 18
        },
        {
          name: "Maryland",
          value: 309
        },
        {
          name: "Maine",
          value: 10
        },
        {
          name: "Michigan",
          value: 54
        },
        {
          name: "Minnesota",
          value: 16
        },
        {
          name: "Missouri",
          value: 3
        },
        {
          name: "Mississippi",
          value: 86
        },
        {
          name: "Montana",
          value: 0
        },
        {
          name: "North Carolina",
          value: 218
        },
        {
          name: "North Dakota",
          value: 0
        },
        {
          name: "Nebraska",
          value: 1
        },
        {
          name: "New Hampshire",
          value: 5
        },
        {
          name: "New Jersey",
          value: 120
        },
        {
          name: "New Mexico",
          value: 41
        },
        {
          name: "Nevada",
          value: 8
        },
        {
          name: "New York",
          value: 365
        },
        {
          name: "Ohio",
          value: 0
        },
        {
          name: "Oklahoma",
          value: 0
        },
        {
          name: "Oregon",
          value: 0
        },
        {
          name: "Pennsylvania",
          value: 0
        },
        {
          name: "Rhode Island",
          value: 0
        },
        {
          name: "South Carolina",
          value: 0
        },
        {
          name: "South Dakota",
          value: 4
        },
        {
          name: "Tennessee",
          value: 40
        },
        {
          name: "Texas",
          value: 61
        },
        {
          name: "Utah",
          value: 22
        },
        {
          name: "Vermont",
          value: 13
        },
        {
          name: "Virginia",
          value: 302
        },
        {
          name: "Washington",
          value: 141
        },
        {
          name: "Wisconsin",
          value: 112
        },
        {
          name: "West Virginia",
          value: 3
        },
        {
          name: "Wyoming",
          value: 67
        }
      ]
    };
  },
  methods: {
    _chartInit(options) {
      this.myChart = echarts.init(document.querySelector(".point .main"));
      console.log(options);
      this.myChart.setOption(this.options);
      this.$root.charts.push(this.myChart);
      window.addEventListener(
        "resize",
        function() {
          this.myChart.resize();
        }.bind(this)
      );
    },
    _getCityData() {
      axios.get("static/data/cityData.json").then(res => {
        this.geoCoordMap = res.data;
        this.$nextTick(() => {
          this._getMyChart();
        });
      });
    },
    _getMyChart() {
      // axios.get("static/data/point/testData.json").then(res => {
      this.options = {
        // backgroundColor: '#404a59',
        title: {
          show: false
        },
        tooltip: {
          trigger: "item",
          showDelay: 0,
          transitionDuration: 0.2,
          formatter: function(params) {
            var value = (params.value + "").split(".");
            value = value[0].replace(/(\d{1,3})(?=(?:\d{3})+(?!\d))/g, "$1,");
            return params.seriesName + "<br/>" + params.name + ": " + value;
          }
        },
        visualMap: {
          show: false,
          left: "left",
          min: -1000,
          max: 1000,
          inRange: {
            color: ["#feca57", "#b33939"]
          },
          text: ["High", "Low"], // 文本，默认为数值文本
          textStyle: {
            color: "#fff"
          },
          calculable: true
        },
        geo: {
          // map: "usa",
          // type: "map",
          roam: true,
          label: {
            emphasis: {
              show: true
            }
          },
          zoom: 1.5,
          // top: 50,
          itemStyle: {
            normal: {
              color: "white",
              opacity: 0.7,
              borderColor: "rgba(0, 0, 0, 1)"
            },
            emphasis: {
              color: "blue"
            }
          }
        },
        toolbox: {
          show: false,
          left: "left",
          top: "top",
          feature: {
            dataView: { readOnly: false },
            restore: {},
            saveAsImage: {}
          }
        },
        series: [
          {
            name: "",
            type: "map",
            roam: true,
            map: "usa",
            zoom: 1.4,
            left: 150,
            top: 80,
            emphasis: {
              label: {
                show: true
              }
            },
            data: this.option_data
          }
        ]
      };
      this._chartInit(this.options);
      // });
    },

    changeOption() {
      if (this.radio1 === "Positive") {
        console.log("Positive");
        this.option_data = [
          {
            name: "Alaska",
            value: 0
          },
          {
            name: "Alabama",
            value: 93
          },
          {
            name: "Arkansas",
            value: 8
          },
          {
            name: "Arizona",
            value: 0
          },
          {
            name: "California",
            value: 202
          },
          {
            name: "Colorado",
            value: 36
          },
          {
            name: "Connecticut",
            value: 36
          },
          {
            name: "Delaware",
            value: 297
          },
          {
            name: "Florida",
            value: 40
          },
          {
            name: "Georgia",
            value: 21
          },
          {
            name: "Hawaii",
            value: 28
          },
          {
            name: "Idaho",
            value: 3
          },
          {
            name: "Illinois",
            value: 74
          },
          {
            name: "Indiana",
            value: 37
          },
          {
            name: "Iowa",
            value: 4
          },
          {
            name: "Kansas",
            value: 32
          },
          {
            name: "Kentucky",
            value: 31
          },
          {
            name: "Louisiana",
            value: 25
          },
          {
            name: "Massachusetts",
            value: 18
          },
          {
            name: "Maryland",
            value: 309
          },
          {
            name: "Maine",
            value: 10
          },
          {
            name: "Michigan",
            value: 54
          },
          {
            name: "Minnesota",
            value: 16
          },
          {
            name: "Missouri",
            value: 3
          },
          {
            name: "Mississippi",
            value: 86
          },
          {
            name: "Montana",
            value: 0
          },
          {
            name: "North Carolina",
            value: 218
          },
          {
            name: "North Dakota",
            value: 0
          },
          {
            name: "Nebraska",
            value: 1
          },
          {
            name: "New Hampshire",
            value: 5
          },
          {
            name: "New Jersey",
            value: 120
          },
          {
            name: "New Mexico",
            value: 41
          },
          {
            name: "Nevada",
            value: 8
          },
          {
            name: "New York",
            value: 365
          },
          {
            name: "Ohio",
            value: 0
          },
          {
            name: "Oklahoma",
            value: 0
          },
          {
            name: "Oregon",
            value: 0
          },
          {
            name: "Pennsylvania",
            value: 0
          },
          {
            name: "Rhode Island",
            value: 0
          },
          {
            name: "South Carolina",
            value: 0
          },
          {
            name: "South Dakota",
            value: 4
          },
          {
            name: "Tennessee",
            value: 40
          },
          {
            name: "Texas",
            value: 61
          },
          {
            name: "Utah",
            value: 22
          },
          {
            name: "Vermont",
            value: 13
          },
          {
            name: "Virginia",
            value: 302
          },
          {
            name: "Washington",
            value: 141
          },
          {
            name: "Wisconsin",
            value: 112
          },
          {
            name: "West Virginia",
            value: 3
          },
          {
            name: "Wyoming",
            value: 67
          }
        ];
        this._getMyChart();
      } else if (this.radio1 === "Negative") {
        console.log("Negative");
        this.option_data = [
          {
            name: "Alabama",
            value: 116
          },
          {
            name: "Alaska",
            value: 0
          },
          {
            name: "Arizona",
            value: 0
          },
          {
            name: "Arkansas",
            value: 11
          },
          {
            name: "California",
            value: 114
          },
          {
            name: "Colorado",
            value: 131
          },
          {
            name: "Connecticut",
            value: 131
          },
          {
            name: "Delaware",
            value: 612
          },
          {
            name: "Florida",
            value: 11
          },
          {
            name: "Georgia",
            value: 32
          },
          {
            name: "Hawaii",
            value: 7
          },
          {
            name: "Idaho",
            value: 0
          },
          {
            name: "Illinois",
            value: 246
          },
          {
            name: "Indiana",
            value: 236
          },
          {
            name: "Iowa",
            value: 3
          },
          {
            name: "Kansas",
            value: 13
          },
          {
            name: "Kentucky",
            value: 71
          },
          {
            name: "Louisiana",
            value: 52
          },
          {
            name: "Maine",
            value: 58
          },
          {
            name: "Maryland",
            value: 798
          },
          {
            name: "Massachusetts",
            value: 27
          },
          {
            name: "Michigan",
            value: 32
          },
          {
            name: "Minnesota",
            value: 8
          },
          {
            name: "Mississippi",
            value: 22
          },
          {
            name: "Missouri",
            value: 11
          },
          {
            name: "Montana",
            value: 0
          },
          {
            name: "Nebraska",
            value: 1
          },
          {
            name: "Nevada",
            value: 0
          },
          {
            name: "New Hampshire",
            value: 12
          },
          {
            name: "New Jersey",
            value: 32
          },
          {
            name: "New Mexico",
            value: 37
          },
          {
            name: "New York",
            value: 705
          },
          {
            name: "North Carolina",
            value: 102
          },
          {
            name: "North Dakota",
            value: 0
          },
          {
            name: "Ohio",
            value: 0
          },
          {
            name: "Oklahoma",
            value: 0
          },
          {
            name: "Oregon",
            value: 0
          },
          {
            name: "Pennsylvania",
            value: 0
          },
          {
            name: "Rhode Island",
            value: 0
          },
          {
            name: "South Carolina",
            value: 0
          },
          {
            name: "South Dakota",
            value: 2
          },
          {
            name: "Tennessee",
            value: 28
          },
          {
            name: "Texas",
            value: 113
          },
          {
            name: "Utah",
            value: 29
          },
          {
            name: "Vermont",
            value: 4
          },
          {
            name: "Virginia",
            value: 745
          },
          {
            name: "Washington",
            value: 101
          },
          {
            name: "West Virginia",
            value: 22
          },
          {
            name: "Wisconsin",
            value: 36
          },
          {
            name: "Wyoming",
            value: 28
          }
        ];
        this._getMyChart();
      } else {
        console.log("Neutral");
        this.option_data = [
          {
            name: "Alaska",
            value: 0
          },
          {
            name: "Alabama",
            value: 67
          },
          {
            name: "Arkansas",
            value: 12
          },
          {
            name: "Arizona",
            value: 0
          },
          {
            name: "California",
            value: 253
          },
          {
            name: "Colorado",
            value: 97
          },
          {
            name: "Connecticut",
            value: 97
          },
          {
            name: "Delaware",
            value: 317
          },
          {
            name: "Florida",
            value: 112
          },
          {
            name: "Georgia",
            value: 46
          },
          {
            name: "Hawaii",
            value: 86
          },
          {
            name: "Idaho",
            value: 7
          },
          {
            name: "Idaho",
            value: 7
          },
          {
            name: "Iowa",
            value: 4
          },
          {
            name: "Illinois",
            value: 92
          },
          {
            name: "Indiana",
            value: 83
          },
          {
            name: "Kansas",
            value: 43
          },
          {
            name: "Kentucky",
            value: 64
          },
          {
            name: "Louisiana",
            value: 31
          },
          {
            name: "Maine",
            value: 15
          },
          {
            name: "Maryland",
            value: 347
          },
          {
            name: "Massachusetts",
            value: 8
          },
          {
            name: "Michigan",
            value: 8
          },
          {
            name: "Minnesota",
            value: 11
          },
          {
            name: "Mississippi",
            value: 62
          },
          {
            name: "Missouri",
            value: 0
          },
          {
            name: "Montana",
            value: 0
          },
          {
            name: "Nebraska",
            value: 2
          },
          {
            name: "Nevada",
            value: 1
          },
          {
            name: "New Hampshire",
            value: 333
          },
          {
            name: "New Jersey",
            value: 67
          },
          {
            name: "New Mexico",
            value: 22
          },
          {
            name: "New York",
            value: 361
          },
          {
            name: "North Carolina",
            value: 274
          },
          {
            name: "North Dakota",
            value: 1
          },
          {
            name: "Ohio",
            value: 0
          },
          {
            name: "Oklahoma",
            value: 0
          },
          {
            name: "Oregon",
            value: 0
          },
          {
            name: "Pennsylvania",
            value: 0
          },
          {
            name: "Rhode Island",
            value: 0
          },
          {
            name: "South Carolina",
            value: 0
          },
          {
            name: "Tennessee",
            value: 115
          },
          {
            name: "Texas",
            value: 174
          },
          {
            name: "Utah",
            value: 49
          },
          {
            name: "Vermont",
            value: 24
          },
          {
            name: "Virginia",
            value: 354
          },
          {
            name: "Washington",
            value: 202
          },
          {
            name: "West Virginia",
            value: 40
          },
          {
            name: "Wisconsin",
            value: 106
          },
          {
            name: "Wyoming",
            value: 38
          }
        ];
        this._getMyChart();
      }
    }
  },
  components: {
    "v-header": header,
    "v-filter": filter
  }
};
</script>
