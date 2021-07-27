<template>
    <div class="container">
        <div class="container-inner">
                <input  class="checkbox" v-on:click='changeCompleted(todo)' type="checkbox" name="" id="">
            <h2 v-bind:class='{done: completed}' v-if='!editTodo'>
                 {{(index+1) + ' '+ todo.title}}
            </h2>
            <input class='form-control' v-else type="text" v-model="todo.title">
            <button class="btn btn-primary" v-on:click="ChangeEditTodos()">Edit</button>
            <button v-on:click='deleteTodo' class="btn btn-outline-dark">X</button>
        </div>
        
    </div>
</template>

<script>
export default{
    props:['todo', 'index'],
    data(){
        return{
            editTodo:false,
            completed: false,
        }
    },
    methods:{
        ChangeEditTodos(){
            this.editTodo= !this.editTodo;
            
        }, 
        changeCompleted(todo){
            todo.completed = !todo.completed;
            this.completed = !this.completed
        },
        deleteTodo(){
            
            this.$emit('deleteTodo', this.todo.id)
        }
    }
}
</script>

<style scoped>
 .container{
     display: flex;
     justify-content: center; 
 }
 .input{
     text-align: center;
 }
 .container-inner{
     display: flex;
    align-items: center;
    border:1px solid grey;
    margin: 5px;
    border-radius: 8px;
 }
 .form-control{
     width: 500px;
 }
 .btn{
     margin: 15px ;
 }
 h2{
     width: 500px;
 }
 .checkbox{
     margin: 15px;
    width: 100px;
 }
 .done{
     text-decoration: line-through;
 }
</style>
