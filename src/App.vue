<template>
  <div id="app">
    <TodoBoard :todos="todos" :addTodo="addTodo" :deleteTodo="deleteTodo" :changeStatusTodo="changeStatusTodo" />
  </div>
</template>

<script>
import TodoBoard from './components/TodoBoard.vue';

export default {
  name: 'App',
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
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    changeStatusTodo(index) {
      this.todos[index].completed = !this.todos[index].completed;
    },
  },
};
</script>
