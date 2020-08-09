<template>
  <div>
    <AddTodo v-on:add-todo="addTodo"/>
   <Todos v-bind:todos="todos" v-on:del-todo="deleteItem" />
  </div>
</template>

<script>

import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';

import axios from 'axios';

export default {
  name:'Home',
  components: {
    Todos,
    AddTodo
    
  },
  data() {
    return {
      // todos:[
      //   {
      //     id:1,
      //     title: "go to shopping",
      //     completed: false
      //   },
      //   {
      //     id:2,
      //     title: "Learn VueJS",
      //     completed: true
      //   }
      //   ,
      //   {
      //     id:3,
      //     title: "Make app",
      //     completed: false
      //   }

      // ]

      todos:[]
      
    }
  },
  methods: {

    deleteItem(id){
    //  this.todos=this.todos.filter(todo=>todo.id!=id);
    axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    .then(this.todos=this.todos.filter(todo=>todo.id!=id))
   
    .catch(err=>console.log(err));

    }

    ,

    addTodo(newTodo){
      // this.todos=[...this.todos,newTodo];
    
      const {title,completed}=newTodo;
    
      axios.post("https://jsonplaceholder.typicode.com/todos",{
        title,
        completed
      })
      .then(res=>this.todos=[...this.todos,res.data])
      .catch(err=>console.log(err));
    }
    
  },
  created:function(){

    axios.get("https://jsonplaceholder.typicode.com/todos?_limit=6")
    .then(response=>this.todos=response.data)
    .catch(err=>console.log(err));
   
  }
}

</script>

<style>

*{
  box-sizing: border-box;
  margin: 0;
  padding:0;
}


.btn{
    display:inline-block;
    border: none;
    cursor: pointer;
    padding: 8px;
    color: #ccc;
    background-color:#0d0d0d;
}

</style>>

