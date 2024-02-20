<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.completed" @change="toggleStatus">
    <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
    <button class="delete-button" @click="deleteTodoItem">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
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
  methods: {
    deleteTodoItem() {
      this.deleteTodo(this.index);
    },
    toggleStatus() {
      this.changeStatusTodo(this.index);
    },
  },
};
</script>

<style scoped>
.todo-item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
}

.completed {
  text-decoration: line-through;
}

.status-indicator {
  margin-left: 10px;
  color: #888;
}

.delete-button {
  padding: 5px 10px;
  font-size: 14px;
  background-color: #dc3545;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #c82333;
}
</style>

