<template>
  <div class="hello">
   
    <span>{{ num }}</span>
    <button @click="add()">点击</button>
    我是:{{ miku }} {{ msg }}
    <button @click="biu()">测试调用</button>
  </div>
</template>

<script >
import { ref } from 'vue';
export default {
  name:'app',
  //获取父组建传过来的变量 和 自定义方法
  props:['miku','msg'],
  emits:['biubiu'],
  //vue3通过setup定义变量  使用ref()的变量可以动态改变  并且通过对象.value来获取值
  //setup可以添加两个参数一个是父组建传过来的值，一个是context对象
  setup(props,context){
    let num = ref(1);
    let person = ref({
      name : 'miku',
      age : 14
    })
    console.log("我是props对象")
    console.log(props)

     console.log(context); //插槽
    function add(){
      console.log(num.value++)
      // ${num};
      console.log(person.value)
      console.log(person.value.name) //显示miku
    }
    //可以通过context去调用父组件的方法
    function biu(){
      context.emit('biubiu',666);
    }

    return{
      num,
      add,
      biu
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
