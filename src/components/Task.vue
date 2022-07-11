<template>
  <div class="ml-10 h-screen relative w-9/12 md:w-6/12 md:m-auto pt-20 ">
    <h1 class="text-4xl text-white opacity-80 m-auto w-full text-center mb-8 ">To Do:</h1>
    <InputTask @addTask = "addTask" />
    <TaskBox :Tasks="data.Tasks" @deleteTasks="deleteTasks"/>
  </div>
  
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import InputTask from './Input-Task.vue';
import DeleteTask from './Delete-Task.vue';
import TaskBox from './Task-Box.vue'


const data:any = reactive({
  Tasks:[],
})


const addTask = (task:any) => {
  data.Tasks.push(task)
}

const deleteTasks = (selectedTasks:number[]) =>{
  selectedTasks.forEach((selectTask: any) => data.Tasks.splice(data.Tasks.findIndex((object:any) => {
  return object.taskId === selectTask
}),1))
  selectedTasks=[]
}





</script>

<style>

</style>