<template>
  <div id="app">
    <p>{{notDone}} tasks remaining</p>
    <TodoList v-bind:AllTodos="todos" :deletethat="deleteTask" />
    <input type="text" v-model="newItem" v-on:keydown.enter="addTodo" />
    <button @click="addTodo">Add</button>
    <p v-if="showError">Please enter Something to add</p>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
export default {
  data(){return{
    todos:[
      {id:1, content:'Köp bananaaa', done:true},
      {id:2, content:'Köp choklad', done:false},
      {id:3, content:'Köp mjölk', done:false},
      {id:4, content:'Köp yogurt', done:true}
    ],
    newItem:'',
    showError:false
  }},
    updated(){
    if(!localStorage.getItem('todolist')){
      localStorage.setItem('todolist',JSON.stringify(this.todos))
    }
    else{
      this.todos=JSON.parse(localStorage.getItem('todolist'))
    }
  },
 components:{TodoList},
 methods:{
   addTodo(){
     if(this.newItem!=''){
       this.todos.push({id:this.total+1, content:this.newItem, done:false})
       this.newItem=''
       this.showError=false
     }
     else{
       this.showError=true
     }
   },
   deleteTask(id){
     if(id){
       this.todos.splice(id-1,1)
     }
   }
 },
 computed:{
   total(){
     return this.todos.length
   },
   notDone(){
     return this.todos.filter(todo=>!todo.done).length
   }
 }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>