<template>
  <div class="todo-item">
    <input type="checkbox" v-on:change="markComplete">
    <p v-bind:class="{'is-complete':todo.completed}">{{todo.title}}</p>
    <button class="del" v-on:click="$emit('del-todo', todo.id)">x</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props:["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>

<style scoped>
  .todo-item {
    display: flex;
    align-items: center;
    background: #f4f4f4;
    padding: 1rem;
    border-bottom: 0.1rem #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 0.5rem 0.9rem;
    border-radius: 50%;
    cursor: pointer;
   margin-left: auto;
  }
</style>