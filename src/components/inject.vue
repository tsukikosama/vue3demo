<template>
  <div>
    666
     {{ car }}
  </div>
</template>

<script>
import { inject } from 'vue'
export default {
    setup(){
        let car = inject('car')

        return {
            car
        };
    }
}
</script>

<style>

</style>