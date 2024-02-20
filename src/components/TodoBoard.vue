<template>
  <div>
    <!-- Todo form -->
    <form @submit.prevent="addNewTodo">
      <input type="text" v-model="newTodoText" placeholder="Enter a new todo">
      <button type="submit">Add Todo</button>
    </form>

    <!-- Todo list -->
    <TodoItem v-for="(todo, index) in todos" :key="index" :todo="todo" :index="index" :deleteTodo="deleteTodo" :changeStatusTodo="changeStatusTodo" />
  </div>
</template>

<script>
import TodoItem from './TodoItems.vue';

export default {
  name: 'TodoBoard',
  components: {
    TodoItem,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
    addTodo: {
      type: Function,
      required: true,
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
    changeStatusTodo: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      newTodoText: '',
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodoText.trim() === '') return;
      this.addTodo({
        text: this.newTodoText,
        completed: false,
      });
      this.newTodoText = '';
    },
  },
};
</script>
