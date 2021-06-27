<template>
  <div>
    <AddTodo @add-todo="addTodo"/>
    <Todos :todos="todos" @delete-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'

export default {
  name: 'Hpme',
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    async getTodos() {
      const res = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5');
      const data = await res.json();
      this.todos = data;
    },
    async addTodo(newTodo) {
      const res = await fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST',
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(newTodo)
      });
      const data = await res.json();
      this.todos = [...this.todos, data];
    },
    async deleteTodo(id) {
      await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        method: 'DELETE'
      });
      this.todos = this.todos.filter(todo => todo.id != id)
    }
  },
  created() {
    this.getTodos();
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border:none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
