<template>
  <div class="todo-board">
    <h2>Todos</h2>

    <form @submit.prevent="addNewTodo" class="add-todo-form">
      <input type="text" v-model="newTodoText" placeholder="Enter a new todo" class="todo-input">
      <button type="submit" class="add-todo-button">Add Todo</button>
    </form>

    <div class="todo-container">
      <div v-for="(todo, index) in todos" :key="index" class="todo-item">
        <TodoItem :todo="todo" :index="index" :deleteTodo="deleteTodo" :changeStatusTodo="changeStatusTodo" />
      </div>
    </div>
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
      newTodoDate: '',
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodoText.trim() === '') return;
      this.addTodo({
        text: this.newTodoText,
        completed: false,
        date: this.newTodoDate,
      });
      this.newTodoText = '';
      this.newTodoDate = '';
    },
  },
};
</script>

<style scoped>
.todo-board {
  background-color: rgb(198, 198, 198);
  margin: 0 auto;
}

h2 {
  text-align: center;
}

.todo-container{
  background-color: aliceblue;
}
.add-todo-form {
  margin-bottom: 20px;
  display: flex;
  margin-left: 4px;
}

.todo-input {
  flex: 1;
  width: 70%;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-todo-button {
  padding: 8px 16px;
  font-size: 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 10px;
  margin-top: 4px;
  margin-right: 4px;
}

.add-todo-button:hover {
  background-color: #0056b3;
}

.todo-container {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px;
}
</style>
