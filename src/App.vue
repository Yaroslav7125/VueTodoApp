<template>
  <div id="app">
    <h1>My todo list!</h1>
    <AddTodo
        v-bind:searchWord="userInput"
        v-on:editSearchWord="userInput = $event"
        v-on:addTodo='PushTodo'
    />
    <TodoList
        v-bind:todos='filteredTodos'
        v-on:deleteTodo="deleteTodo"
        v-on:ChangeTodoCompleted="ChangeTodoCompleted"
        v-on:changeTodoTitle="changeTodoTitle"
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
    AddTodo,
  },
  data() {
    return {
      todos: [
        { id:1,title:'купить хлеп', completed: false},
        { id:2,title:'купить матрас', completed: false},
        { id:3,title:'купить сено', completed: false},
      ],
      userInput: '',
    }
  },
  methods: {
    SetToLocalStorage() {
      localStorage.setItem('todosArr', JSON.stringify(this.todos));
    },
    PushTodo(newTodo) {
      this.todos.push(newTodo);
      this.SetToLocalStorage() // сетим в local Storage
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      this.SetToLocalStorage(); //сетим в local Storage
    },
    ChangeTodoCompleted(index) {
      this.todos[index].completed = !this.todos[index].completed;
      this.SetToLocalStorage(); // сетим при изм completed
    },
    changeTodoTitle(index, StrTitle){
      this.todos[index].title = StrTitle;
      this.SetToLocalStorage();// сетим при изменении title
    }
  },

  computed: {
    filteredTodos: function () {

      if (this.userInput != '') {
        return this.todos.filter(t => t.title.includes(this.userInput))
      } else {
        return this.todos;
      }
    },
  },
  mounted: function () {
    this.$nextTick(function () {

      if (JSON.parse(localStorage.getItem("todosArr"))) {
        this.todosArr = JSON.parse(localStorage.getItem("todosArr"));// читаем
      }
      else localStorage.setItem('todosArr', JSON.stringify(this.todosArr));
    })
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
