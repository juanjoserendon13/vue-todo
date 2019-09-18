<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import fetch from 'isomorphic-fetch'
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
const BASEURL = 'https://jsonplaceholder.typicode.com/todos';
export default {
  name: 'Home',
  components: {
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
    async deleteTodo(id) {
      try {
        const response = await fetch(`${BASEURL}/${id}`, 
        {
          method: 'DELETE',
        }
      );
      const todoDeleted = await response.json();
      this.todos =  this.todos.filter(t => t.id !== id);
      } catch (error) {
        console.log(error);
      }
    },
    async addTodo(newTodo) {
      const {title, completed} = newTodo;
      try {
        const response = await fetch(BASEURL, 
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
      const response = await fetch(`${BASEURL}?_limit=5`);
      const data = await response.json();
      this.todos = data;
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<style>

</style>
