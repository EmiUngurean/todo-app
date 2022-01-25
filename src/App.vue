<template>
<div class="container">
  <div id="app">
    <h1 class="text-center">{{title}}</h1> 

    <div class="submitForm">

     <input type="text" v-model="todo" name="todo" placeholder="Enter task..."  class="f">
     <input type="date" name="currentDate" v-model="myDate">
     <button @click="addEvent" class="addBtn">Add event</button>
  
    </div>
 

    <table class="table">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Date</th>
      <th scope="col">Edit task</th>
      <th scope="col">Remove task</th>
      <th scope="col">Over task</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(element, index) in tasks" :key="index">
    <td>    
        <span :class="{done: element.done}" >{{element.todo}}</span>     
    </td>
    <td>
      <span :class="{done: element.done}">{{myDate}}</span>
    </td>
    <td>
      <div class="icons" @click="editTask(index)">
        <span class="fa fa-pen"></span>
      </div>
    </td>
    <td>
       <div class="icons" @click="deleteTask(index)"> 
        <span class="fa fa-trash"></span>
      </div>
    </td>
    <td>
      <div class="icons" @click="markAsDoneTask(element)" id="done">
        <span class="fa fa-check"></span>
      </div>
    </td>
    </tr>
   
  </tbody>
</table>
 </div>  
</div>  

</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      id: Date.now(),
      editedEvent:null,
      title: 'Todo App!',
      todo:'', //object insert in input
      tasks: [], //tasks is my list of objects
      done: false,
      currentData:{myDate: new Date().toISOString().slice(0,10)},
    
    }
  },
  methods: {
    addEvent(){
      if(this.todo.length==0 || this.currentData==0) return  alert('Please insert your task and the date!')    
      if(this.editedEvent==null){
          this.tasks.push({todo:this.todo,done:false}) 
          
      }
      else{
        this.tasks[this.editedEvent].todo = this.todo
        this.editedEvent=null
      }       
      this.todo='' //clear the input
    },
   editTask(index){
      this.todo = this.tasks[index].todo
      this.editedEvent=index
    },
    deleteTask(index){
      this.tasks.splice(index,1)
    },

    markAsDoneTask(todo){      
      todo.done = !todo.done   
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #6e93b9;
  margin-top: 60px;
  background: rgb(135, 211, 211);

}
input{
  text-align: center;
  border-radius: 12px;
  
}
.icons{
  cursor: pointer;
}
.done{
  text-decoration: line-through;
  color: rgb(255, 30, 0);
}
.addBtn{
border-radius: 12px;

}
/* img{
  cursor:pointer;
  width: 17px;
  height: auto;
} */
</style>
