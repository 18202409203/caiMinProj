<template>
  <div id="pageTwo">
    <el-container>
    <!-- unit1 左边部分 -->
      <el-aside width="514px">
        <el-card class="card1">
          <div slot="header">
            <el-tag hit>实验水箱</el-tag>
          </div>
          <div style="width: 450px">
            <img src="../assets/tank.png" width="100%" height="100%">
          </div>
        </el-card>
      </el-aside>
      <!-- unit2 中间部分 -->
      <el-container>
        <el-aside width="1000px">
          <el-card class="card4">
          <div slot="header">
            <el-tag>模型参数曲线</el-tag>
            <el-button type="text" style="float: right;margin: 2px 5px;" size="mini" @click="bigChartUp">查看详细</el-button>
          </div>
          <div id="chartUp2">
            <chart :styles="chartUpLittle" :options="options1" container="chartUp2"></chart>
          </div>
          </el-card>
          <el-card class="card4">
          <div slot="header">
            <el-tag>输入输出曲线</el-tag>
            <el-button type="text" style="float: right;margin: 2px 5px;" size="mini" @click="bigChartDown">查看详细</el-button>
          </div>
          <div id="chartDown2">
            <chart :styles="chartDownLittle" :options="options2" container="chartDown2"></chart>
          </div>
          </el-card>
        </el-aside>
      <!-- unit3 右边部分 -->
        <el-main>
          <el-card class="card3">
          <div slot="header">
            <el-tag>性能评价</el-tag>
          </div>
          <div style="margin-top: 50px;">
            <el-table
              border :show-header="false"
              :data="tableData"
              style="width: 100%">
              <el-table-column
                align="center"
                prop="left">
              </el-table-column>
              <el-table-column
                align="center"
                prop="right">
              </el-table-column>
            </el-table>
          </div>
          </el-card>
          <el-card style="height: 200px; margin: 10px;">
          <div slot="header">
            <el-tag>控制按钮</el-tag>
          </div>
          <div style="margin: 0 85px;">
            <el-button type="primary" class="downButton" :disabled="disabled1" @click="changeColor(1)">物理对象监控</el-button>
            <el-button type="primary" class="downButton" :disabled="disabled2" @click="changeColor(2)">仿真对象监控</el-button>
          </div>
          </el-card>
        </el-main>
      </el-container>
    </el-container>
    <el-dialog :fullscreen="true" :visible.sync="chartVisibleUp2">
        <div id="chartUpBig2">
          <chart :options="options1" :styles="chartUpBig2" container="chartUpBig2"></chart>
        </div>
    </el-dialog>
    <el-dialog :fullscreen="true" :visible.sync="chartVisibleDown2">
        <div id="chartDownBig2">
          <chart :options="options2" :styles="chartDownBig2" container="chartDownBig2"></chart>
        </div>
    </el-dialog>
  </div>
</template>
<script>
import chart from "../components/chart.vue";
export default {
  components: { chart },
  props: ["disabled"],
  watch: {
    disabled() {
      if (this.disabled === true) {
        this.$el.style.display = "none";
      } else {
        this.$el.style.display = "inline";
      }
    }
  },
  mounted() {
    if (this.disabled === true) {
      this.$el.style.display = "none";
    } else {
      this.$el.style.display = "inline";
    }
  },
  data() {
    return {
      disabled1: false,
      disabled2: false,
      // 曲线图高和宽
      chartUpLittle: { height: 280, width: 940 },
      chartUpBig2: { height: 800, width: 1600 },
      chartDownLittle: { height: 280, width: 940 },
      chartDownBig2: { height: 800, width: 1600 },
      options1: {
        title: {
          text: "水箱液位值与设定值曲线"
        },
        yAxis: {
          title: {
            text: "水箱液位"
          },
          min: 0,
          max: 25,
          lineWidth: 1
          // plotLines: [
          //   {
          //     color: "#000",
          //     dashStyle: "Dash", //Dash,Dot,Solid,默认Solid
          //     width: 1.5,
          //     value: 14, //y轴显示位置
          //     zIndex: 5
          //   }
          // ]
        },
        chart: {
            type: 'line',
            zoomType: 'xy',
            resetZoomButton: {
                position: {
                    // align: 'right', // by default
                    // verticalAlign: 'top', // by default
                    x: 0,
                    y: -30
                }
            }
        },
        xAxis: {
          min: 0,
          max: 2000,
          // 基准线
          //   　　plotLines: [{   //一条延伸到整个绘图区的线，标志着轴中一个特定值。
          //         color: '#000',
          //         dashStyle: 'Dash', //Dash,Dot,Solid,默认Solid
          //         width: 1.5,
          //         value: 4.5,  //x轴显示位置，一个标记为1
          //         zIndex: 5
          //     }],
        },
        // 图例
        legend: {
          enabled: false
        },
        // legend: {
        //   layout: "vertical",
        //   align: "right",
        //   verticalAlign: "middle"
        // },
        plotOptions: {
          series: {
            label: {
              connectorAllowed: false
            }
          }
        },
        series: [
          {
            name: "实际液位",
            // 这里是数据
            data: []
          },
          // {a
          //   name: "设定值",
          //   data: [14]
          // }
        ],
        responsive: {
          rules: [
            {
              condition: {
                maxWidth: 500
              },
              chartOptions: {
                legend: {
                  layout: "horizontal",
                  align: "center",
                  verticalAlign: "bottom"
                }
              }
            }
          ]
        },
        credits: {
          enabled: false
        }
      },
       options2: {
        title: {
          text: "误差曲线"
        },
        // subtitle: {
        //     text: ''
        // },
        yAxis: {
          title: {
            text: "水箱液位"
          },
          max: 25,
          min: 0,
          // lineColor: '#000000',
          lineWidth: 1
          // plotLines: [
          //   {
          //     color: "#000",
          //     dashStyle: "Dash", //Dash,Dot,Solid,默认Solid
          //     width: 1.5,
          //     value: 14, //y轴显示位置
          //     zIndex: 5
          //   }
          // ]
        },
        chart: {
            type: 'line',
            zoomType: 'xy',
            resetZoomButton: {
                position: {
                    // align: 'right', // by default
                    // verticalAlign: 'top', // by default
                    x: 0,
                    y: -30
                }
            }
        },
        xAxis: [
          // 基准线
          //   　　plotLines: [{   //一条延伸到整个绘图区的线，标志着轴中一个特定值。
          //         color: '#000',
          //         dashStyle: 'Dash', //Dash,Dot,Solid,默认Solid
          //         width: 1.5,
          //         value: 4.5,  //x轴显示位置，一个标记为1
          //         zIndex: 5
          //     }],
          {max: 2000, min: 0}
        ],
        legend: { // 图例
          enabled: false
        },
        plotOptions: {
          series: {
            label: {
              connectorAllowed: false
            }
          }
        },
        series: [
          {
            name: "实际液位",
            // 这里是数据
            data: []
          }
        ],
        responsive: {
          rules: [
            {
              condition: {
                maxWidth: 500
              },
              chartOptions: {
                legend: {
                  layout: "horizontal",
                  align: "center",
                  verticalAlign: "bottom"
                }
              }
            }
          ]
        },
        credits: {
          enabled: false
        }
      },
      chartVisibleUp2: false,
      chartVisibleDown2: false,
      tableData: [
        {
          left: "超调量",
          right: "XXX"
        },
        {
          left: "稳态误差",
          right: "XXX"
        },
        {
          left: "响应时间",
          right: "XXX"
        },
        {
          left: "波动均方差",
          right: "XXX"
        },
        {
          left: "积分均方差",
          right: "XXX"
        },
        {
          left: "误差均方差",
          right: "XXX"
        }
      ]
    }
  },
  methods: {
    bigChartUp() {
      this.chartVisibleUp2 = true;
    },
    bigChartDown() {
      this.chartVisibleDown2 = true;
    },
      changeColor ( flag ) {
          switch (flag) {
            case 1 :
              this.disabled1 = true
              this.disabled2 = false
              break
            case 2 :
              this.disabled1 = false
              this.disabled2 = true
              break
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card1 {
  /* height: 420px; */
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card2 {
  height: 632px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card3 {
  height: 480px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card4 {
  height: 340px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card5 {
  height: 200px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.leftButton {
  /* text-align: center; */
  /* display: flex; */
  margin: 35px 5px 5px 32px;
}
.middleButton {
  /* text-align: center; */
  width: 150px;
  margin: 10px 12px 10px 12px;
}
.downButton {
  margin: 10px 21px 10px 21px;
}
.input {
  left: 10px;
  width: 100px;
}

/* ---------------------------------*/

.el-aside,
.el-main {
  background-color: #d3dce6;
  color: #333;
  padding: 0 !important;
  /* text-align: center; */
  /* line-height: 200px; */
}

/*----------------------------*/
.el-button--primary.is-disabled {
  background: gray;
  border-color: gray;
}
</style>
