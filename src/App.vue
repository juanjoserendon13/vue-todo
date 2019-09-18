<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import fetch from 'isomorphic-fetch'
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [

      ]
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos =  this.todos.filter(t => t.id !== id);
    },
    async addTodo(newTodo) {
      const {title, completed} = newTodo;
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos', 
        {
          method: 'POST',
          body: JSON.stringify({title,completed}),
          headers:{
            'Content-Type': 'application/json'
          }
        }
      );
      const todoCreated = await response.json();
      this.todos = [...this.todos, todoCreated];
      } catch (error) {
        console.log(error);
      }
    }
  },
  async created() {
    // This will be fire as soon as the component get mounted
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5');
      const data = await response.json();
      this.todos = data;
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    border: none;
    background-color: #555;
    color: #fff;
    padding: 0.7rem 2rem;
    cursor: pointer;
  }
  .btn:hover {
    background-color: #666;
  }
</style>
