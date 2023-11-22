<template>
    <div><button @click="testBtn">test</button>{{result}}<br/><br/>
        x : <input type="text" v-model.number="data.x"/><br/>
        y : <input type="text" v-model.number="data.y"/>
        <button @click="clickBtn">click</button>{{result}}<br/><br/>
        x : <input type="text" v-model.number="data2.x"/><br/>
        y : <input type="text" v-model.number="data2.y"/>
        <button @click="clickBtn2">click</button>{{data2.result}}<br/><br/>

        x : <input type="text" v-model.number="data3"/><br/>
        y : <input type="text" v-model.number="data3"/>{{ result3 }}
        <br/><br/>
        data4.x : <input type="text" v-model.number="data4.x"/>
        data4.result : <input type="text" v-model.number="data4.result"/>
        <br/>

        x2 : <input type="text" v-model.number="x2"/><br/>
        y2 : <input type="text" v-model.number="y2"/>{{ result2 }}
        <br/><br/>
        x4 : <input type="text" v-model.number="x4"/><br/>
        y4 : <input type="text" v-model.number="y4"/>{{ result4 }}
        <button @click="watchBtn">watchBtn</button>
    </div>
</template>

<script>
// import { computed } from '@vue/reactivity';
import { computed, reactive, ref, watch, watchEffect } from 'vue';

    export default {
        name : "Calc",
        setup(){
            const data = ref({x : 10, y: 20});
            const result = computed(()=>data.value.x+data.value.y);
            const clickBtn = ()=>{console.log(result.value);}

            const data2 = reactive({x : 30, y : 80, result : 30 + 70});
            const clickBtn2 = ()=>{data2.result = data2.x + data2.y; console.log(data2.result);}

            // const data3 = reactive({x : 1000, y:3000});
            const data3 = ref(100);
            const result3 = ref(data3.value * 2);
            watch(data3, (c, o)=> {
                console.log(`${c} ${c} before ${o} ${o}`);
                result3.value = c * 2;
            });
            const testBtn = () => {data3.value = 100}
            const data4 = reactive({x : 0 , result : 0});
            watch(()=> data4.x, (c, o) => {
                console.log(`${c} ${c}`);
                data4.result++;
            });

            const x2 = ref(10);
            const y2 = ref(20);
            const result2 = ref(x2.value + y2.value);
            watch([x2, y2], ([cx, cy], [ox, oy]) => {
                console.log(`${cx} ${ox}`);
                console.log(`${cy} ${oy}`);
                result2.value = cx + cy;
            });

            const x4= ref(10);
            const y4= ref(20);
            const result4 = ref(0);

            const watchFunc = watchEffect(()=>{
                result4.value = x4.value + y4.value;
                console.log(`${x4.value} ${y4.value}`);
            });

            const watchBtn = ()=>{
                watchFunc();
            }

            return {data,  result, clickBtn, data2, clickBtn2, data3, result3, testBtn, data4, x2, y2, result2, x4, y4, result4, watchBtn}

            // return {
            //     x : ref(10),
            //     y : ref(20)
            // }
        }
    }
</script>

<style scoped>

</style>