<template>
    <span>
        {{ car }}
    </span>
    <Inject/>
</template>

<script>
import { inject } from 'vue'
import Inject from './inject.vue'
export default {
    components:{Inject},
    setup(){
        let car = inject('car')

        return {
            car
        }
    }
}
</script>

<style>

</style>