<template>
  <div id="app">
    <TodoBoard :todos="todos" @addTodo="addTodo" @deleteTodo="deleteTodo" @changeStatusTodo="changeStatusTodo" />
  </div>
</template>

<script>
import TodoBoard from "./components/TodoBoard.vue";

export default {
  name: "App",
  components: {
    TodoBoard,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId);
    },
    changeStatusTodo(todoId) {
      const todoIndex = this.todos.findIndex(todo => todo.id === todoId);
      this.todos[todoIndex].completed = !this.todos[todoIndex].completed;
    },
  },
};
</script>

<style>


</style>
