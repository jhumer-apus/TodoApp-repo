<template>
  <div class="flex items-center h-16 md:h-24">
    <input type="text" v-model="Task.inputTask" v-on:keyup.enter="addTask" class="h-full w-full md:text-3xl text-xl focus:outline-0 pl-4 opacity-80 rounded-l-sm">
    <button @click="addTask" class="w-24 bg-white opacity-80 h-full text-3xl md:ml-2 ml-1  rounded-r-sm px-3.5s "> &#43;</button><br>
  </div>
  
</template>

<script setup lang="ts">

import { reactive } from "vue";

const emits = defineEmits(["addTask"]);


let Task:any = reactive({
  taskId:0,
  inputTask:""
  
})

const addTask = () => {
    if(Task.inputTask.trim().length !== 0){
      Task.taskId++
      emits("addTask", {taskId:Task.taskId, taskText:Task.inputTask})
      Task.inputTask = ""
    }
    Task.inputTask = ""
}


</script>

<style scoped>

</style>>

