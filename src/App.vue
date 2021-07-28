<template>
  <div id="app">
    <h1>My todo list!</h1>
    <AddTodo
        v-bind:searchWord="searchWordApp"
        v-on:editSearchWord="searchWordApp = $event"
        v-on:addTodo='PushTodo'

    />
    <TodoList
        v-bind:todos='TheSearchWordApp'
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
  data() {
    return {
      todosArr: [],
      searchWordApp: '',
    }
  },
  methods: {

    PushTodo(newTodo) {

      this.todosArr.push(newTodo);
      localStorage.setItem(todosArr, JSON.stringify(this.todosArr)); // сетим в local Storage
    },
    deleteTodo(id) {
      this.todosArr = this.todosArr.filter(t => t.id !== id);
      //localStorage.setItem(todosArr, JSON.stringify(this.todosArr)); // сетим при удалении
    },
  },

  computed: {
    TheSearchWordApp: function () {
      console.log(this.searchWordApp)
      //return this.searchWordApp
      if (this.searchWordApp != '') {
        return this.todosArr.filter(t => t.title.includes(this.searchWordApp))
      } else {
        return this.todosArr.filter(t => t.title.includes(this.searchWordApp))
      }

    },
  },
  mounted: function () {
    this.$nextTick(function () {


      if (JSON.parse(localStorage.getItem("todosArr")))
        this.todosArr = JSON.parse(localStorage.getItem("todosArr"));// читаем
      else localStorage.setItem(todosArr, JSON.stringify([]));

      //console.log(typeof array); // объект
      //console.log(array); // [1, 2, 3]
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
