<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="firstPage">
      <first-page :disabled="firstDisabled"></first-page>
    </div>
    <!-- 第二个界面 -->
    <div id="secondPage">
      <second-page :disabled="secondDisabled"></second-page>
    </div>
    <!-- 底部footer -->
    <el-container>
      <el-footer>
        <div style="text-align: center;">
          <span>-</span>
          <button @click="goFirstPage">1</button>
          <button @click="goSecondPage">2</button>
          <span>-</span>
        </div>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import firstPage from '../components/firstPage.vue'
import secondPage from '../components/secondPage.vue'
export default {
  name: 'HelloWorld',
  components: {firstPage, secondPage},
  data () {
    return {
      msg: '双容水箱未建模动态控制实验',
      firstDisabled: true,
      secondDisabled: false
    }
  },
  methods: {
    goFirstPage () {
      // console.log('1')
      this.msg = '双容水箱未建模动态控制实验'
      this.firstDisabled = false
      this.secondDisabled = true
    },
    goSecondPage () {
      // console.log('2')
      this.msg = '递推最小二乘辨识实验'
      this.firstDisabled = true
      this.secondDisabled = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
    text-align: center;
  }

</style>
