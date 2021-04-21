<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo($event)"/>
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(index) {
      this.todos.splice(index, 1);
      // this.todos = this.todos.filter((todo, todoIndex) => {
      //   return todoIndex !== index;
      // });
      // this.todos = this.todos.filter((todo, todoIndex) => todoIndex !== index-1);
    },
    addTodo (newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res => {
          this.todos = [...this.todos, res.data]
        })
        .catch(err => console.log(err));

    }
  },
  created () {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => {
      this.todos = res.data
    })
    .catch(err => console.log(err));
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }  

  .btn:hover {
    background: #666;
  }
</style>
