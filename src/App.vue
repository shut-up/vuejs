<template>
  <div id="app">
    <p v-text="title"></p>

    <!-- 子组件传参给父组件 -->
    <p>son tell me : {{messagefromson}} </p>

    <!-- 双向绑定数据 v-model标签 -->
    <input v-model="newItem" v-on:keyup.enter="addItem">
    <li v-for="item in items" v-bind:class="{isFinish : item.isFinished}"  v-on:click="toggleFinish(item)">
      {{item.label}}
    </li>

    <!-- 父组件传参给子组件 -->
    <child messageforfather="you die!" v-on:listenToMySonMethods="listenToMySon"></child>
  </div>
</template>

<script>
//  导入组件
  import Storage from './store'
  import child from './components/child'

  export default {
    //初始化属性值
    data: function () {
      return {
        title: 'the thing to do ',
        items: Storage.fetch(),
        newItem: '',
        messagefromson: ''
      }
    },
    //注册child组件，否则<child>标签会报错找不到
    components:{ child },

//    监听items属性的变化，发生变化就执行下面的方法
    watch: {
      items: {
        //将items保存到localstorage
        handler: function (items) {
          Storage.save(items)
        }
      }
    },
    methods: {
      //点击切换事项是否完成
      toggleFinish: function (item) {
        item.isFinished = !item.isFinished
      },
      //添加代办事项
      addItem: function () {
        this.items.push({
          label: this.newItem,
          isFinished: false
        })
        this.newItem = ''   //置空
      },
      //子组件传递过来的值通过msg参数接受
      listenToMySon: function (msg) {
        this.messagefromson = msg;
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .isFinish{
    text-decoration: underline;
  }
</style>
