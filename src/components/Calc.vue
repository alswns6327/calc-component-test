<template>
    <div>
        x : <input type="text" v-model.number="x"/><br/>
        y : <input type="text" v-model.number="y"/>
        <button @click="clickBtn">click</button>{{result}}
    </div>
</template>

<script>
import { computed } from '@vue/reactivity';
import { ref } from 'vue';

    export default {
        name : "Calc",
        setup(){
            const x = ref(10);
            const y = ref(20);
            const result = computed(()=>x.value+y.value);
            const clickBtn = ()=>{console.log(result.value);}
            return {x, y,  result, clickBtn}

            // return {
            //     x : ref(10),
            //     y : ref(20)
            // }
        }
    }
</script>

<style scoped>

</style>