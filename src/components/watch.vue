<template>
    <h1>当前求和为:{{ sum }}</h1>
   <button @click="sum++">点我加一</button>
   <hr/>
   <h2>当前的信息为:{{ msg }}</h2>
   <button @click="msg += '!'">修改信息</button>
   <hr/>
   <h2>姓名:{{ person.name }}</h2>
   <h2>年龄:{{ person.age }}</h2>
   <h2>薪资:{{ person.job.j1.salary }}K</h2>
  <button @click="person.name = person.name + '~'">修改姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">增长薪资</button>
</template>

<script>
import { ref, reactive, watch } from 'vue';
export default {
    name : 'watch',

    setup(){
        let sum = ref(0);
        let msg = ref('你好');
        let person = reactive({
        name: '张三',
        age: 18,
        job:{
            j1:{
            salary: 20
            }
        }
        })
        //1 监视ref定义的普通对象
        // watch(sum,(newVal,oldVal) => {
        //     console.log(newVal),
        //     console.log(oldVal)
        // },{
        //     //监视的配置
        //    immediate: true //一上来就更新 
        // });
        //2 监视ref的多个对象
        // watch([sum,msg],(nv,ov) =>{
        //     console.log('sum的值或者msg的值发生变化了');
        //    console.log(`newValue:${nv}, oldValue:${ov}`);
        // },{
        //     //监视的配置
        //    immediate: true //一上来就更新 
        // })
        //3.监视reactive定义的对象
        // 没有办法获取正确的oldvalue
        // 强制开起了深度监控
        // watch(person,(nv,ov)=>{
        //     console.log(nv)
        //     console.log("old" )
        //     console.log(ov)
        // },{
        //     deep:false
        //     // immediate: true //一上来就更新 
        // })
        //4. 监控reactive定义的对象的某个属性
        // watch(()=>person.age,(nv,ov) =>{
        //     console.log(nv),
        //     console.log(ov)
        // })
        //5.监控reactive中的某些属性
        //  watch([() => person.age, () => person.name], (nv, ov) => {
        //       //此时nv和ov都是数组
        //       console.log('person的age或name发生改变了',nv, ov);
        //     });

        //特殊情况
        watch( person.job, (nv, ov) => {
        //这里依然无法拿到正确的ov，因为依然监视的是对象
         console.log('person的job信息发生改变了',nv, ov);
        }, {
        //这里必须要加deep:true注意
            deep: true //此处因为监视的是reactive所定义的响应式对象的一个属性(这个属性的值它依然是一个对象)，所以deep配置有效
        })
        return{
            sum,
            msg,
            person,
            watch
            
        }
    },

    //1
    

}
</script>

<style>

</style>