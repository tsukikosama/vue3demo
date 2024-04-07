<template v-slot:asd>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <HelloWorld msg="Welcome to Your Vue.js App" miku="i miku" @biubiu="show"/>
  <hr/>
  <Reactive/>

   <h6>计算属性</h6>
   <Computed/>
   <h6>监视器</h6>
   <Watch/>
   <h1>hook</h1>
   <Hookdemo/>
  <h1>自定义ref</h1>
   <input v-model="keyWord"/>
  <h3>{{ keyWord }}</h3>
  <h1>
    provide
  </h1>
  <span>{{ name }} {{ price }}</span>
  <Provide/>
  <h1>teleport</h1>
  <Teleports/>
  <br>

  <span>suspense</span>
  <Suspense>
      <template v-slot:default>
        <Child/>
      </template>
      <template v-slot:fallback>
        <!--退路-->
        <h3>loading...</h3>
      </template>
    </Suspense>
    <Mysuspense/>
</template >

<script>
//
import HelloWorld from './components/HelloWorld.vue'
import Reactive from './components/reactive.vue'
import Computed from './components/computed.vue'
import Watch from './components/watch.vue'
import Hookdemo from './components/hookdemo.vue'
import Provide from './components/provide.vue'
import Teleports from './components/myteleport.vue'

import {ref , customRef, reactive, provide, toRefs,readonly,isRef, isReactive, isReadonly, isProxy,defineAsyncComponent} from 'vue'
const Mysuspense = defineAsyncComponent(() => import('./components/mysuspense')); //动态引入组件(异步)
export default {
  name: 'App',
  components: {
    HelloWorld,
    Reactive,
    Computed,
    Watch,
    Hookdemo,
    Provide,
    Teleports,
    Mysuspense
  },

  setup(){
    //使用自定义ref
    let keyWord = myRef('hellw');


    //自定义ref(customRef)
    function myRef(val){
      return customRef((track, trigger) =>{
        let timer ;
        return{
          get(){
            console.log(`从myRef这个容器读取数据，data:${val}`);
            track();//通知追踪value的变化 (和getter商量一下让他明确这个val有用)
            return val;
          },
          set(nv){
            console.log(`从myRef这个容器读取数据，data改为${nv}`);
            clearTimeout(timer);
            timer = setTimeout(() => {
                val = nv;
                trigger() //trigger通知vue重新解析
            }, 500);
          }
        }
      })
    };
    //使用reactive传递数据 子组件和子组件的子组件都可以获取到
    let car = reactive({
      name : 'b',
      price : 40
    });
    
    provide('car',car)

  
    let sum = ref(0);

    let car2 = readonly(car); ///readonly依然返回代理类型的对象只不过它不能再改而已

    console.log(isRef(sum), isReactive(car), isReadonly(car2), isProxy(car), isProxy(car2), isProxy(sum));
    return{
      ...toRefs(car),
      // car,
      keyWord,
      show(val){
        console.log("app show:" +val)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
