<template>
  <div id="hello">
    <h1>{{msg}}</h1>
    <h2>{{this.messageforfather}}</h2>
    <button v-on:click="onClickMe">open mouse!</button>
  </div>
</template>

<script>
  export default {
    data: function () {
      return {
        msg: 'hello world!'
      }
    },
    props: ['messageforfather'],  //接受父组件传过来的messageforfather属性
    //响应父组件的listenToMySon方法
    methods: {
      onClickMe: function () {
        //第一个参数为监听父组件的方法属性，第二个参数为传递到父组件的属性值
         this.$emit('listenToMySonMethods',this.msg)
      }
    }
  }
</script>

<style scoped>
  h1{
    color: #42b983;
  }
</style>
