<template>
  <div id="pageTwo">
    <el-container>
    <!-- unit1 左边部分 -->
      <el-aside>
        <el-card class="card1">
          <div slot="header">
            <el-tag hit>实验水箱</el-tag>
          </div>
          <div>
            <img src="../assets/tank.png" width="100%" height="100%">
          </div>
        </el-card>
        <el-card class="card5">
          <div slot="header">
            <el-tag>模型参数估计结果</el-tag>
          </div>
          <div>
            <el-form>
              <el-form-item label="K1">
                <el-input style="margin-left: 20px;width: 180px;"></el-input>
              </el-form-item>
              <el-form-item label="K2">
                <el-input style="margin-left: 20px;width: 180px;"></el-input>
              </el-form-item>
              <el-form-item label="K3">
                <el-input style="margin-left: 20px;width: 180px;"></el-input>
              </el-form-item>
              <el-form-item label="K4">
                <el-input style="margin-left: 20px;width: 180px;"></el-input>
              </el-form-item>
            </el-form>
          </div>
        </el-card>
      </el-aside>
      <!-- unit2 中间部分 -->
      <el-container>
        <el-aside style="width: 520px;">
        <el-card class="card2">
          <div slot="header">
            <el-tag>双容水箱机理模型</el-tag>
          </div>
          <div style="padding: 35px; display: inline; color: #fff;"></div>
          <img src="../assets/img1.png" height="110px">
        </el-card>
        <el-card class="card2">
          <div slot="header">
            <el-tag>双容水箱离散模型</el-tag>
          </div>
          <div style="padding: 20px; display: inline; color: #fff;"></div>
          <img src="../assets/img2.png" height="110px">
        </el-card>
        <el-card class="card2">
          <div slot="header">
            <el-tag>辨识算法</el-tag>
          </div>
          <div style="padding: 35px; display: inline; color: #fff;"></div>
          <img src="../assets/img3.png" height="110px">
        </el-card>
        <el-card class="card2">
          <div slot="header">
            <el-tag>仿真模型</el-tag>
          </div>
          <img src="../assets/img4.png">
        </el-card>
        </el-aside>
      <!-- unit3 右边部分 -->
        <el-main>
          <el-card class="card4">
          <div slot="header">
            <el-tag>模型参数曲线</el-tag>
            <el-button type="text" style="float: right;margin: 2px 5px;" size="mini" @click="bigChartUp">查看详细</el-button>
          </div>
          <div id="chartUp1">
            <chart :styles="chartUpLittle" :options="options1" container="chartUp1"></chart>
          </div>
          </el-card>
          <el-card class="card4">
          <div slot="header">
            <el-tag>输入输出曲线</el-tag>
            <el-button type="text" style="float: right;margin: 2px 5px;" size="mini" @click="bigChartDown">查看详细</el-button>
          </div>
          <div id="chartDown1">
            <chart :styles="chartDownLittle" :options="options2" container="chartDown1"></chart>
          </div>
          </el-card>
        </el-main>
      </el-container>
    </el-container>
    <el-dialog :fullscreen="true" :visible.sync="chartVisibleUp1">
        <div id="chartUpBig1">
          <chart :options="options1" :styles="chartUpBig1" container="chartUpBig1"></chart>
        </div>
    </el-dialog>
    <el-dialog :fullscreen="true" :visible.sync="chartVisibleDown1">
        <div id="chartDownBig1">
          <chart :options="options2" :styles="chartDownBig1" container="chartDownBig1"></chart>
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
      // 曲线图高和宽
      chartUpLittle: { height: 300, width: 1024 },
      chartUpBig1: { height: 800, width: 1600 },
      chartDownLittle: { height: 300, width: 1024 },
      chartDownBig1: { height: 800, width: 1600 },
      // 数据
      options1: {
        title: {
          text: "模型参数曲线"
        },
        // subtitle: {
        //     text: ''
        // },
        yAxis: {
          type: 'linear',
          title: {
            text: "水箱液位"
          },
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
          type: "line",
          zoomType: "xy",
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
            name: "y1",
            // 这里是数据
            data: [14.4, 18.4, 14.39, 15.39]
          },
          {
            name: "y2",
            // 这里是数据
            data: [26.4, 20.4, 26.39, 23.39]
          },
          {
            name: "u",
            // 这里是数据
            data: [12.4, 32.4, 23.39, 31.39]
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
      options2: {
        title: {
          text: "输入输出曲线"
        },
        // subtitle: {
        //     text: ''
        // },
        yAxis: {
          title: {
            text: "水箱液位"
          },
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
          type: "line",
          zoomType: "xy",
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
            name: "K1",
            data: [14.4, 14.4, 14.39, 16.39]
          },
          {
            name: "K2",
            data: [12.3, 4.56, 12.3, 34.4]
          },
          {
            name: "K3",
            data: [6.2, 13.4, 16.4, 14.39]
          },
          {
            name: "K4",
            data: [6.2, 6.2, 14.39, 21.39]
          },
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
      chartVisibleUp1: false,
      chartVisibleDown1: false,
    };
  },
  methods: {
    bigChartUp() {
      this.chartVisibleUp1 = true;
    },
    bigChartDown() {
      this.chartVisibleDown1 = true;
    },
    changeColor(flag) {
      switch (flag) {
        case 1:
          this.disabled1 = true;
          this.disabled2 = false;
          this.disabled3 = false;
          break;
        case 2:
          this.disabled1 = false;
          this.disabled2 = true;
          this.disabled3 = false;
          break;
        case 3:
          this.disabled1 = false;
          this.disabled2 = false;
          this.disabled3 = true;
          break;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card1 {
  /* height: 480px; */
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card2 {
  height: 180px;
  width: 500px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card3 {
  height: 270px;
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card4 {
  height: 370px;
  /* width: 100%; */
  /* border: 1px #000 solid; */
  margin: 10px;
}
.card5 {
  height: 340px;
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
