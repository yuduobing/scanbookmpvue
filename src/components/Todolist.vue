<template>
  <div class="wrapper">
    <p>{{title}}</p>{{asads}}
    <p v-if="show">{{subTitle}}</p>
    <div>
      <input type="text" v-model="mytodo">
      <button @click="handleClick"> 添加</button>

      <button @click=" deletea">删除</button>

    </div>
    <ul>
      <!--style动态变化  更改一个属性-->
      <!--<li  :style="{'text-decoration':todo.done?'line-through':''}"  @click="change(index)"  v-for="(todo,index) in todos" >{{todo.text}}{{index+1}}</li>-->

      <li  :class="{'done':todo.done}"  :key="index" @click="change(index)"  v-for="(todo,index) in todos" >{{todo.text}}{{index+1}}</li>
    </ul>

    <p> {{remain}}/{{todos.length}}</p>

  </div>
</template>

<script>
  /* eslint-disable no-unused-expressions */

  export default {

    data () {
      return {
        title: '你好',
        subTitle: '我是可以影藏的内容',
        showSub: true,
        mytodo: '',
        todos: [
          {text: '吃饭', done: false},
          {text: '写代码', done: false},
          {text: '吃饭', done: false}
        ]
      }
    },
    computed: {
      remain () {
        // 过滤以及完成的false
        return this.todos.filter(v => !v.done).length
      }
    },
    methods: {
      // 添加单个  ,s数组添加
      // handleClick () {
      //   this.todos.push(this.mytodo)
      //   this.mytodo = ''
      // },
      // 添加单个   集合添加
      handleClick () {
        this.todos.push({text: this.mytodo, done: false})
        this.mytodo = ''
      },
      change (i) {
        this.todos[i].done = !this.todos[i].done
      },
      deletea () {
        this.todos = []
      }

    },
  }
</script>
<style>
  li.done{
    text-decoration:line-through;
    color: red;
  }
</style>

