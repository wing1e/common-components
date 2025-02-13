<template>
    <div class="container" >
        <div class="list-scroll" @scroll="handeScrool">
            <div class="list" :style="{transform:`translateY(${offset}px)`,height:`${data.length*50-startIndex*50}px`}">
                <div class="list-item" v-for="item in randarList" :key="item">{{ 'item'+item }}</div>
            </div>
            
        </div>
    </div>
</template>
<script setup>
import { computed, ref } from 'vue';

let data = Array.from({length:20},(_,i)=>i)

const maxCount = 9
// 起始索引
const startIndex = ref(0)
// 结束索引
const endIndex = ref(0)
// 滚动条距离其顶部的距离
const scrollTop = ref(0)


const offset = computed(()=>{
    return startIndex.value * 50
})

const randarList = computed(()=>{
   
    return data.slice(startIndex.value,endIndex.value==0?maxCount:endIndex.value)
})

const addData = ()=>{
    data.push(...Array.from({length:10},(_,i)=>i+data.length))
    
    
}


const handeScrool = (e)=>{
   // e.target.scrollHeight 滚动条高度
   // e.target.scrollTop 滚动条距离其顶部的距离（以px为单位）
   scrollTop.value = e.target.scrollTop
   startIndex.value = Math.floor(scrollTop.value/50)
   console.log(e.target.scrollTop ,scrollTop.value);
   
   if(endIndex.value==data.length-2){
    addData()
   }
   endIndex.value = startIndex.value+maxCount
    
}

</script>
<style>
    *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    }
    .container{
        width: 200px;
        height: 400px;
        border: 1px solid black;
        margin: 0 auto;
        .list-scroll{
            width: 100%;
            height: 100%;
            overflow: auto;
            .list{
            width: 100%;
            .list-item{
                width: 100%;
                height: 50px; 
                line-height: 50px;
                background-color: antiquewhite;
                border: 1px solid black;
            }
        }
        }
       
    }
</style>