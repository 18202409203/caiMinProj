<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
  padding: 0;
  margin: 0;
}
  .el-card__header {
    background-color: #000;
    padding: 0!important;
  }
   .el-input.is-disabled .el-input__inner {
   color: #000!important;
   cursor: default!important;
 }
  h1, h2 {
    font-weight: normal;
    text-align: center;
  }
</style>
