<template>
    <div class="content">

        
        

        <Todo 
        v-for="(todo, index) in todos"
        v-bind:todo='todo'
        v-bind:index='index'

        v-on:deleteTodo="deleteTodo"
        />


        
        
        
    </div>
</template>

<script>
import Todo from './Todo.vue'
export default{
    props:['todos'],
    components:{
        Todo:Todo
    },
    methods:{
        deleteTodo(id){
            this.$emit('deleteTodo', id);
        }
    }
}
</script>


<style scoped>

</style>
