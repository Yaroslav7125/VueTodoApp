<template>
  <div id="app">
    <h1>My todo list!</h1>  
    <AddTodo
      v-on:addTodo='PushTodo'
      v-on:search='search'
    />
    <TodoList
    v-bind:todos='todosArr'
    v-on:deleteTodo="deleteTodo"
    />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import AddTodo from './components/AddTodo.vue'

export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo
    
  },
  data(){
    return {
      todosArr:[],
      tempSearchTodo:[],
    }
  },
  methods:{
    PushTodo(newTodo){
        this.todosArr.push(newTodo);
    },
    deleteTodo(id){
      this.todosArr = this.todosArr.filter(t=>t.id !==id);
    },
    /* search(){
      
    } */
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
