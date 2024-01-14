<script lang="ts">
    import { defineComponent } from 'vue';
    type Result = {
        btn: string,
    }
    export default defineComponent({
        data(){
            return {
                result: [
                        {btn: "C"}, {btn: "("}, {btn: ")"}, {btn: "*"},
                        {btn: "7"}, {btn: "8"}, {btn: "9"}, {btn: "/"},
                        {btn: "4"}, {btn: "5"}, {btn: "6"}, {btn: "+"},
                        {btn: "1"}, {btn: "2"}, {btn: "3"}, {btn: "-"},
                        {btn: "."}, {btn: "0"}, {btn: "00"},{btn: "="}
                    ] as Result[],
                value: "0"
            }
        },
        methods: {
            handleBtn(data: string){
                if(this.value == "0"){
                    this.value = data
                }else{
                    this.value = this.value + data
                }
            },
            handleClear(){
                this.value = "0"
            },
            handleResult(){
                try {
                    const result = eval(this.value)
                    this.value = result
                } catch (error) {
                    this.value = "Error"
                }
            }
        }
    })
</script>
<template>
    <div class="bg-[#112D4E] h-screen">
        <div class="flex justify-center">
            <div class="basis-1/3 bg-[#3F72AF] p-10 rounded-2xl">
                <form action="">
                    <input type="text" name="" id="" class="w-full h-20 rounded-2xl text-4xl text-end pe-3" v-bind:value="value" />
                    <div class="grid grid-cols-4 gap-4 mt-4">
                        <div v-for="i in result">
                            <button 
                                type="button" 
                                class="aspect-square w-full bg-[#DBE2EF] text-[#112D4E] font-bold rounded-xl text-2xl"
                                v-if="i.btn == 'C'"
                                v-on:click="handleClear()"
                                >{{ i.btn }}
                            </button>
                            <button 
                                type="button" 
                                class="aspect-square w-full bg-[#DBE2EF] text-[#112D4E] font-bold rounded-xl text-2xl"
                                v-else-if="i.btn == '='"
                                v-on:click="handleResult()"
                                >{{ i.btn }}
                            </button>
                            <button 
                                type="button" 
                                class="aspect-square w-full bg-[#DBE2EF] text-[#112D4E] font-bold rounded-xl text-2xl"
                                v-else
                                v-on:click="handleBtn(i.btn)"
                                >{{ i.btn }}
                            </button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>