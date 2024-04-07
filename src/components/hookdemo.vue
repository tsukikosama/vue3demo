<template>
  <h1>{{ sum }}</h1>
  <button @click="sum++">点击</button>
  <h2>鼠标点击的坐标 x:{{ point.x }}, Y:{{ point.y }}</h2>
</template>

<script>
import {ref} from 'vue'
import usePoint from '../hooks/usePoint'
export default {
    name : 'hookdemo',
    setup(){

        let sum = ref(0);

        const point = usePoint();

        return{
            sum,
            point
        }
    }
}
</script>

<style>

</style>