<template>
    <div class="container">
            <div class="container-inner">
                <input class='form-control' type="text" v-model='valueTodo'>
                
                <button v-on:click='makeTodo' class="btn btn-warning">Add</button>
                 <input class='form-control form-control-search' v-model='searchWord' placeholder="Search..."  type="text" > 
                <!--  <button v-on:click='SearchTodo' class="btn btn-warning">Search</button> --> 
            </div>
    </div>
</template>
<script>
export default{
    data(){
        return{
            valueTodo:'',
            searchWord:'',
        }
    },
    methods:{
        makeTodo(){
            if(this.valueTodo){
                let strValue = this.valueTodo;
                const NewTodo = {
                    id:Date.now(),
                    title: strValue,
                    completed:false,
                    filterS:true,
                }
                this.$emit('addTodo', NewTodo);
            } 
            this.valueTodo='';
        },
    },
    watch:{
            searchWord:function(){
                this.$emit('search', this.searchWord);
            }
        }
}

</script>
<style scoped>
.container{
    display: flex;  
    justify-content: center;
}
.container-inner{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-left: 20px;
    border:1px solid grey;
    margin: 5px;
    border-radius: 3px;   
}
.form-control{
     width: 500px;
 }
 .form-control-search{
     width: 100px;
     margin-right: 15px;
 }
 .btn{
     margin: 15px ;
 }

</style>
