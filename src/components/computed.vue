<template>
    姓:<input type="text" v-model="person.name">
    <br>
    名:<input type="text" v-model="person.lastname">
    <p>姓名：{{ person.username }}</p>
    修改全名:<input type="text" v-model="person.username">
</template>

<script>
import {reactive , computed} from 'vue'
export default {
    name : 'computed',   
    setup(){
        let person = reactive({
            name : 'miku',
            lastname : 'cywl',
            age : 14
        })
        //计算方法的修改和获取
        person.username = computed({
            get(){
                return person.name + '-' + person.lastname
            },
            set(name){
                let [fn ,ln] = name.split('-');
                person.name = fn,
                person.lastname = ln;
            }

        })
        return{
            person
        }
    }
}
</script>

<style>

</style>