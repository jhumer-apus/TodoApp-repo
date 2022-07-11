<template>
    <div  class="mt-4  text-white flex items-center justify-between opacity-80">
      <label class="text-xl md:text-3xl">
        <input type="checkbox" v-model="data.selectAllTasks" @change="selected" class="w-4 h-4 md:w-5 md:h-5">
          Select All
      </label>
      <div>
        <button @click="deleteTasks" class="right-0 p-2" :disabled="data.selectTask.length<1"><span class="text-4xl md:text-5xl">&#128465;</span></button>
      </div>
      
    </div>
    <div class="overflow-auto h-4/6 border-t-2 border-white opacity-80">
      <transition-group name="list" :v-if="props.Tasks.length>0" v-for="task in props.Tasks" :key ="task.taskId" tag="ul">
        <li class="taskItem  w-full bg-white hover:bg-slate-300 mt-6 list-none flex">
          <label class="pl-8 py-4 text-xl w-full h-full cursor-pointer break-words md:text-3xl md:py-8">
          <input type="checkbox"  class="text-right w-4 h-4 mr-4 rounded md:w-5 md:h-5" v-model="data.selectTask" :value="task.taskId">
           {{task.taskText}}
         </label><br>
       </li>   
       </transition-group>
     </div>

    

</template>

<script setup lang="ts">

import { reactive, ref,watch } from 'vue'

const props = defineProps<{
  Tasks:any
}>();

const emits = defineEmits(["deleteTasks"]);

const data:any = reactive({
  selectAllTasks:false,
  selectTask:[],
})


const selected = () =>{
  if(data.selectAllTasks){
    data.selectTask = props.Tasks.map((task:any)=> task.taskId)
    console.log(data.selectTask)
  }
  else {
   data.selectTask = [];
  }
}

const deleteTasks =()=>{
  emits("deleteTasks", data.selectTask)
  data.selectTask=[]
  data.selectAllTasks = false
}

</script>

<style scoped>

.input[type="checkbox"]:hover:after {
  background-image: linear-gradient(135deg, #8BB0C2 0%, #FFF 100%);
  border-color: #85A9BB #92C2DA #92C2DA #85A9BB;
}
.list-move{
  transition: transform 1s;
}
.taskItem {
  animation-name: fade-in;
  animation-duration: 0.5s;
}

@keyframes fade-in {
  from {opacity: 0;}
  to {opacity: 0.8;}
}


</style>