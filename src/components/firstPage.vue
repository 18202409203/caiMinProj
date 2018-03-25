<template>
  <div id="pageTwo">
    <el-container>
    <!-- unit1 左边部分 -->
      <el-aside width="514px">
        <el-card class="card1">
          <div slot="header">
            <el-tag hit>算法原理</el-tag>
          </div>
          <div style="width: 450px">
            <img src="../assets/algorithmPrinciple.png" width="100%" height="100%">
          </div>
        </el-card>
        <el-card class="card5">
          <div slot="header">
            <el-tag>实验控制</el-tag>
          </div>
          <div>
            <el-button @click="changeColor(1)" :disabled="disabled1" type="primary" class="leftButton">启动实验</el-button>
            <el-button @click="changeColor(2)" :disabled="disabled2" type="primary" class="leftButton">停止实验</el-button>
            <el-button @click="changeColor(3)" :disabled="disabled3" type="primary" class="leftButton">退出实验</el-button>
          </div>
        </el-card>
      </el-aside>
      <!-- unit2 中间部分 -->
      <el-container>
        <el-aside width="600px">
        <el-card class="card2">
          <div slot="header">
            <el-tag>参数设定</el-tag>
          </div>
          <div>
            <el-button type="primary" class="middleButton">U=U1</el-button>
            <el-button type="primary" class="middleButton">U=U1+U2</el-button>
            <el-button type="primary" class="middleButton">U=U1+U2+U3</el-button>
          </div>
          <div style="margin: 25px 25px 25px 25px; border: 1px #000 solid; border-radius: 10px;padding-top: 20px;">
              <el-form label-position="right" label-width="200px">
                <el-form-item :label="items[0].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[0].inputValue" class="input"></el-input>
                </el-form-item>
                <el-form-item :label="items[1].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[1].inputValue" class="input"></el-input>
                </el-form-item>
                <el-form-item :label="items[2].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[2].inputValue" class="input" ></el-input>
                </el-form-item>
                <el-form-item :label="items[3].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[3].inputValue" class="input" ></el-input>
                </el-form-item>
                <el-form-item :label="items[4].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[4].inputValue" class="input" ></el-input>
                </el-form-item>
                <el-form-item :label="items[5].displayValue + ':'">
                  <el-input placeholder="XXX" v-model="items[5].inputValue" class="input"></el-input>
                </el-form-item>
              </el-form>
          </div>
          <div>
            <el-button type="primary" class="downButton">参数自动化</el-button>
            <el-button type="primary" class="downButton">自动</el-button>
            <el-button type="primary" class="downButton">手动</el-button>
            <el-button type="primary" class="downButton">参数下载</el-button>
          </div>
        </el-card>
        </el-aside>
      <!-- unit3 右边部分 -->
        <el-main>
          <el-card class="card3">
          <div slot="header">
            <el-tag>性能评价</el-tag>
          </div>
          <div>
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
          <el-card class="card4">
          <div slot="header">
            <el-tag>状态曲线</el-tag>
            <el-button type="text" style="float: right;margin: 2px 5px;" size="mini" @click="bigChart">查看详细</el-button>
          </div>
          <div id="chart11">
            <chart :styles="chart1Little" :options="options1" container="chart11"></chart>
          </div>
          </el-card>
        </el-main>
      </el-container>
    </el-container>
    <el-dialog :fullscreen="true" :visible.sync="chartVisible">
        <div id="chart12">
          <chart :options="options1" :styles="chart1Big" container="chart12"></chart>
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
      disabled3: false,
      chart1Little: { height: 300, width: 480 },
      chart1Big: { height: 800, width: 1600 },
      options1: {
        title: {
          text: "水箱状态曲线"
        },
        // subtitle: {
        //     text: ''
        // },
        yAxis: {
          title: {
            text: "水箱液位"
          },
          plotLines: [
            {
              color: "#000",
              dashStyle: "Dash", //Dash,Dot,Solid,默认Solid
              width: 1.5,
              value: 14, //y轴显示位置
              zIndex: 5
            }
          ]
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
          // 基准线
          //   　　plotLines: [{   //一条延伸到整个绘图区的线，标志着轴中一个特定值。
          //         color: '#000',
          //         dashStyle: 'Dash', //Dash,Dot,Solid,默认Solid
          //         width: 1.5,
          //         value: 4.5,  //x轴显示位置，一个标记为1
          //         zIndex: 5
          //     }],
        },
        legend: {
          layout: "vertical",
          align: "right",
          verticalAlign: "middle"
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
            data: [
              0,
              1,
              5,
              6,
              10,
              14,
              16.26,
              16.24,
              16.26,
              16.27,
              16.28,
              16.29,
              16.25,
              16.27,
              16.29,
              16.28,
              16.3,
              16.28,
              16.27,
              16.29,
              16.29,
              16.27,
              16.26,
              16.27,
              16.28,
              16.3,
              16.26,
              16.26,
              16.28,
              16.27,
              16.28,
              16.27,
              16.32,
              16.29,
              16.29,
              16.27,
              16.25,
              16.3,
              16.23,
              16.28,
              16.26,
              16.26,
              16.27,
              16.25,
              16.24,
              16.24,
              16.25,
              16.26,
              16.24,
              16.22,
              16.27,
              16.26,
              16.28,
              16.24,
              16.23,
              16.24,
              16.23,
              16.27,
              16.27,
              16.26,
              16.22,
              16.24,
              16.21,
              16.19,
              16.2,
              16.22,
              16.2,
              16.21,
              16.23,
              16.23,
              16.25,
              16.22,
              16.21,
              16.21,
              16.19,
              16.18,
              16.18,
              16.16,
              16.17,
              16.2,
              16.16,
              16.18,
              16.17,
              16.18,
              16.15,
              16.15,
              16.11,
              16.16,
              16.19,
              16.18,
              16.15,
              16.15,
              16.13,
              16.15,
              16.12,
              16.1,
              16.09,
              16.09,
              16.09,
              16.09,
              16.1,
              16.09,
              16.12,
              16.11,
              16.07,
              16.07,
              16.07,
              16.07,
              16.04,
              16.1,
              16.06,
              16.06,
              16.01,
              16.02,
              16.04,
              16.03,
              16.05,
              16.0,
              16.0,
              16.03,
              16.0,
              16.0,
              15.99,
              16.0,
              15.95,
              15.98,
              15.96,
              15.98,
              15.95,
              15.96,
              15.94,
              15.94,
              15.88,
              15.93,
              15.95,
              15.93,
              15.94,
              15.9,
              15.94,
              15.94,
              15.93,
              15.87,
              15.91,
              15.88,
              15.87,
              15.85,
              15.84,
              15.82,
              15.86,
              15.8,
              15.82,
              15.84,
              15.8,
              15.77,
              15.81,
              15.78,
              15.77,
              15.75,
              15.74,
              15.77,
              15.74,
              15.75,
              15.73,
              15.72,
              15.67,
              15.72,
              15.68,
              15.68,
              15.68,
              15.64,
              15.68,
              15.68,
              15.65,
              15.66,
              15.67,
              15.63,
              15.6,
              15.63,
              15.62,
              15.59,
              15.58,
              15.59,
              15.57,
              15.6,
              15.55,
              15.56,
              15.55,
              15.57,
              15.52,
              15.52,
              15.49,
              15.54,
              15.52,
              15.49,
              15.45,
              15.44,
              15.4,
              15.35,
              15.34,
              15.31,
              15.27,
              15.25,
              15.21,
              15.18,
              15.15,
              15.11,
              15.07,
              15.07,
              15.03,
              14.99,
              14.96,
              14.95,
              14.87,
              14.86,
              14.83,
              14.79,
              14.75,
              14.71,
              14.7,
              14.71,
              14.71,
              14.68,
              14.66,
              14.63,
              14.59,
              14.55,
              14.57,
              14.59,
              14.56,
              14.56,
              14.57,
              14.56,
              14.54,
              14.54,
              14.55,
              14.52,
              14.47,
              14.5,
              14.49,
              14.51,
              14.52,
              14.52,
              14.5,
              14.47,
              14.45,
              14.5,
              14.48,
              14.49,
              14.46,
              14.47,
              14.44,
              14.43,
              14.43,
              14.46,
              14.46,
              14.44,
              14.44,
              14.43,
              14.43,
              14.4,
              14.38,
              14.39,
              14.43,
              14.38,
              14.41,
              14.41,
              14.4,
              14.39,
              14.39,
              14.41,
              14.44,
              14.39,
              14.4,
              14.39,
              14.42,
              14.41,
              14.39,
              14.4,
              14.35,
              14.38,
              14.38,
              14.34,
              14.37,
              14.36,
              14.38,
              14.4,
              14.38,
              14.38,
              14.37,
              14.36,
              14.36,
              14.36,
              14.33,
              14.34,
              14.37,
              14.35,
              14.37,
              14.35,
              14.35,
              14.36,
              14.37,
              14.37,
              14.35,
              14.36,
              14.38,
              14.33,
              14.33,
              14.39,
              14.39,
              14.34,
              14.32,
              14.35,
              14.36,
              14.36,
              14.37,
              14.38,
              14.33,
              14.35,
              14.36,
              14.36,
              14.36,
              14.35,
              14.36,
              14.36,
              14.35,
              14.36,
              14.35,
              14.36,
              14.4,
              14.34,
              14.4,
              14.39,
              14.37,
              14.35,
              14.37,
              14.37,
              14.38,
              14.45,
              14.38,
              14.4,
              14.38,
              14.44,
              14.41,
              14.43,
              14.45,
              14.41,
              14.42,
              14.43,
              14.41,
              14.44,
              14.42,
              14.47,
              14.46,
              14.46,
              14.44,
              14.42,
              14.42,
              14.42,
              14.48,
              14.48,
              14.46,
              14.48,
              14.49,
              14.49,
              14.43,
              14.41,
              14.45,
              14.47,
              14.43,
              14.5,
              14.49,
              14.52,
              14.49,
              14.5,
              14.52,
              14.53,
              14.56,
              14.57,
              14.52,
              14.54,
              14.57,
              14.51,
              14.53,
              14.53,
              14.57,
              14.57,
              14.6,
              14.54,
              14.56,
              14.6,
              14.59,
              14.56,
              14.61,
              14.6,
              14.57,
              14.6,
              14.67,
              14.65,
              14.65,
              14.69,
              14.65,
              14.67,
              14.68,
              14.66,
              14.66,
              14.67,
              14.67,
              14.68,
              14.69,
              14.7,
              14.72,
              14.73,
              14.73,
              14.7,
              14.73,
              14.71,
              14.73,
              14.78,
              14.75,
              14.79,
              14.75,
              14.78,
              14.83,
              14.8,
              14.79,
              14.79,
              14.85,
              14.81,
              14.79,
              14.81,
              14.79,
              14.84,
              14.8,
              14.84,
              14.84,
              14.89,
              14.89,
              14.81,
              14.88,
              14.87,
              14.91,
              14.93,
              14.86,
              14.85,
              14.89,
              14.87,
              14.9,
              14.91,
              14.93,
              14.93,
              14.91,
              14.97,
              14.98,
              14.99,
              14.99,
              14.96,
              14.92,
              14.94,
              14.95,
              14.95,
              14.97,
              14.99,
              15.04,
              14.99,
              15.05,
              15.03,
              15.13,
              15.08,
              15.06,
              15.06,
              15.02,
              15.08,
              15.09,
              15.08,
              15.11,
              15.08,
              15.1,
              15.11,
              15.15,
              15.09,
              15.13,
              15.09,
              15.08,
              15.13,
              15.12,
              15.08,
              15.14,
              15.19,
              15.14,
              15.16,
              15.18,
              15.2,
              15.19,
              15.22,
              15.25,
              15.25,
              15.21,
              15.19,
              15.27,
              15.21,
              15.24,
              15.26,
              15.25,
              15.21,
              15.25,
              15.26,
              15.25,
              15.27,
              15.28,
              15.27,
              15.29,
              15.3,
              15.3,
              15.32,
              15.39,
              15.33,
              15.33,
              15.35,
              15.36,
              15.32,
              15.36,
              15.37,
              15.34,
              15.37,
              15.36,
              15.38,
              15.39,
              15.43,
              15.43,
              15.4,
              15.42,
              15.44,
              15.41,
              15.44,
              15.5,
              15.48,
              15.49,
              15.47,
              15.47,
              15.43,
              15.4,
              15.46,
              15.49,
              15.45,
              15.52,
              15.52,
              15.52,
              15.52,
              15.55,
              15.55,
              15.56,
              15.54,
              15.51,
              15.54,
              15.56,
              15.57,
              15.59,
              15.53,
              15.57,
              15.62,
              15.59,
              15.59,
              15.6,
              15.58,
              15.64,
              15.63,
              15.63,
              15.59,
              15.63,
              15.63,
              15.64,
              15.59,
              15.62,
              15.64,
              15.65,
              15.65,
              15.64,
              15.67,
              15.68,
              15.67,
              15.72,
              15.7,
              15.7,
              15.67,
              15.64,
              15.71,
              15.71,
              15.7,
              15.73,
              15.71,
              15.73,
              15.69,
              15.76,
              15.77,
              15.8,
              15.79,
              15.79,
              15.77,
              15.78,
              15.81,
              15.82,
              15.77,
              15.8,
              15.85,
              15.81,
              15.86,
              15.85,
              15.83,
              15.83,
              15.84,
              15.84,
              15.87,
              15.87,
              15.87,
              15.88,
              15.83,
              15.86,
              15.91,
              15.89,
              15.85,
              15.88,
              15.91,
              15.91,
              15.94,
              15.95,
              15.96,
              15.96,
              15.95,
              15.94,
              15.98,
              15.95,
              15.95,
              15.96,
              15.95,
              15.95,
              15.98,
              16.02,
              16.01,
              15.98,
              15.94,
              16.03,
              16.0,
              16.01,
              16.03,
              16.03,
              15.99,
              16.04,
              16.01,
              16.04,
              16.02,
              16.06,
              16.05,
              16.06,
              16.01,
              16.04,
              16.07,
              16.04,
              16.09,
              16.06,
              16.06,
              16.13,
              16.12,
              16.08,
              16.07,
              16.09,
              16.11,
              16.08,
              16.08,
              16.14,
              16.11,
              16.1,
              16.11,
              16.11,
              16.09,
              16.14,
              16.13,
              16.12,
              16.16,
              16.16,
              16.18,
              16.18,
              16.16,
              16.18,
              16.21,
              16.17,
              16.16,
              16.18,
              16.2,
              16.22,
              16.18,
              16.17,
              16.19,
              16.2,
              16.24,
              16.23,
              16.2,
              16.21,
              16.17,
              16.19,
              16.2,
              16.2,
              16.21,
              16.17,
              16.21,
              16.22,
              16.2,
              16.21,
              16.18,
              16.15,
              16.21,
              16.2,
              16.22,
              16.2,
              16.18,
              16.23,
              16.23,
              16.21,
              16.21,
              16.21,
              16.24,
              16.24,
              16.2,
              16.26,
              16.24,
              16.24,
              16.23,
              16.24,
              16.25,
              16.19,
              16.26,
              16.25,
              16.24,
              16.21,
              16.18,
              16.24,
              16.23,
              16.22,
              16.18,
              16.22,
              16.19,
              16.24,
              16.2,
              16.22,
              16.23,
              16.24,
              16.21,
              16.2,
              16.22,
              16.22,
              16.23,
              16.23,
              16.22,
              16.2,
              16.2,
              16.17,
              16.2,
              16.2,
              16.22,
              16.17,
              16.2,
              16.17,
              16.18,
              16.17,
              16.18,
              16.19,
              16.22,
              16.18,
              16.18,
              16.17,
              16.2,
              16.19,
              16.12,
              16.18,
              16.19,
              16.18,
              16.17,
              16.18,
              16.14,
              16.12,
              16.14,
              16.12,
              16.13,
              16.16,
              16.14,
              16.11,
              16.13,
              16.16,
              16.11,
              16.1,
              16.13,
              16.16,
              16.1,
              16.12,
              16.14,
              16.07,
              16.08,
              16.07,
              16.11,
              16.09,
              16.08,
              16.09,
              16.09,
              16.12,
              16.1,
              16.1,
              16.07,
              16.05,
              16.04,
              16.08,
              16.06,
              16.04,
              16.05,
              16.07,
              16.05,
              16.01,
              16.01,
              16.03,
              16.02,
              16.01,
              16.01,
              15.98,
              16.01,
              15.99,
              16.01,
              16.0,
              16.04,
              15.95,
              15.95,
              15.96,
              15.97,
              15.95,
              15.95,
              15.93,
              15.93,
              15.93,
              15.94,
              15.89,
              15.91,
              15.91,
              15.86,
              15.84,
              15.88,
              15.92,
              15.87,
              15.87,
              15.85,
              15.85,
              15.87,
              15.82,
              15.82,
              15.8,
              15.81,
              15.8,
              15.81,
              15.77,
              15.79,
              15.76,
              15.75,
              15.78,
              15.75,
              15.75,
              15.77,
              15.74,
              15.7,
              15.71,
              15.72,
              15.71,
              15.67,
              15.69,
              15.69,
              15.7,
              15.67,
              15.65,
              15.69,
              15.66,
              15.66,
              15.63,
              15.64,
              15.62,
              15.63,
              15.59,
              15.59,
              15.57,
              15.54,
              15.57,
              15.56,
              15.55,
              15.54,
              15.51,
              15.46,
              15.54,
              15.52,
              15.49,
              15.49,
              15.45,
              15.49,
              15.46,
              15.44,
              15.45,
              15.43,
              15.46,
              15.42,
              15.4,
              15.36,
              15.33,
              15.32,
              15.29,
              15.25,
              15.23,
              15.2,
              15.16,
              15.09,
              15.11,
              15.07,
              15.04,
              15.01,
              14.96,
              14.93,
              14.91,
              14.85,
              14.82,
              14.8,
              14.77,
              14.74,
              14.71,
              14.66,
              14.71,
              14.61,
              14.6,
              14.59,
              14.59,
              14.61,
              14.55,
              14.56,
              14.55,
              14.54,
              14.53,
              14.51,
              14.52,
              14.51,
              14.51,
              14.51,
              14.49,
              14.5,
              14.48,
              14.47,
              14.47,
              14.48,
              14.45,
              14.47,
              14.42,
              14.43,
              14.44,
              14.38,
              14.42,
              14.41,
              14.4,
              14.39,
              14.4,
              14.38,
              14.4,
              14.41,
              14.4,
              14.4,
              14.39,
              14.39
            ]
          },
          {
            name: "设定值",
            data: [14]
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
      chartVisible: false,
      items: [
        { displayValue: "比例系数KP", inputValue: "", index: 1 },
        { displayValue: "积分时间KI", inputValue: "", index: 2 },
        { displayValue: "液位设定值", inputValue: "", index: 3 },
        { displayValue: "a1", inputValue: "", index: 4 },
        { displayValue: "b0", inputValue: "", index: 5 },
        { displayValue: "b1", inputValue: "", index: 6 }
      ],
      tableData: [
        {
          left: "液位波动均方差",
          right: "XXX"
        },
        {
          left: "液位积分均方差",
          right: "XXX"
        },
        {
          left: "液位误差均方差",
          right: "XXX"
        },
        {
          left: "液位均值",
          right: "XXX"
        }
      ]
    }
  },
  methods: {
      bigChart () {
          this.chartVisible = true
      },
      changeColor ( flag ) {
          switch (flag) {
            case 1 :
              this.disabled1 = true
              this.disabled2 = false
              this.disabled3 = false
              break
            case 2 :
              this.disabled1 = false
              this.disabled2 = true
              this.disabled3 = false
              break
            case 3 :
              this.disabled1 = false
              this.disabled2 = false
              this.disabled3 = true
              break
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card1 {
  height: 420px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card2 {
  height: 632px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card3 {
  height: 270px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card4 {
  height: 350px;
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
