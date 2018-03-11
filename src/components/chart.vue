<template>
  <div id="highcharts-container"></div>
</template>

<script>
import Highcharts from 'highcharts/highstock';
import HighchartsMore from 'highcharts/highcharts-more';
import HighchartsDrilldown from 'highcharts/modules/drilldown';
import Highcharts3D from 'highcharts/highcharts-3d';
HighchartsMore(Highcharts)
HighchartsDrilldown(Highcharts);
Highcharts3D(Highcharts);

export default {
  props: ['options', 'styles', 'container'],
  name: 'highcharts',
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    let div = document.createElement('div')
    let highChart = document.getElementById(this.container)
    highChart.appendChild(div)
    this.initChart(div);
  },
  methods: {
    initChart(div) {
      // console.log(div);
      div.style.width = (this.styles.width || 800) + 'px';
      div.style.height = (this.styles.height || 400) + 'px';
      this.chart = new Highcharts.Chart(div, this.options);
    }
  }
}
</script>

<style lang="css">
  .highcharts-container {
    width: 800px;
    height: 400px;
  }
</style>