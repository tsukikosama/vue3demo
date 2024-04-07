<template>
    <div class="hello">
     
      <span>{{ num }}</span>
      <button @click="add()">点击</button>
    </div>
  </template>
  
  <script >
  import { reactive } from 'vue';
  export default {
    name:'app',
    //vue3通过reactive定义变量  使用reactive()的变量可以动态改变  并且通过对象来获取值
    //这个和setup的区别 这个适用对象，普通的数据类型 不会响应式
    setup(){
      let num = reactive([1,2,3,4]);
      let person = reactive({
        name : "miku",
        age : 14
      })
      function add(){
        console.log(num[1]++)
        // ${num};
        console.log(person)
        console.log(person.name) //显示miku
      }
  
      return{
        num,
        add
      }
    }
  }
  
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
  </style>
  