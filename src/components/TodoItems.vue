<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.completed" @change="toggleStatus">
    <span :class="{ completed: todo.completed }" class="todo-text">{{ todo.text }}</span>
    <button class="delete-button" @click="deleteTodoItem">Delete</button>
    <button class="edit-button" @click="editTodoItem">Edit</button>
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
    editTodo: {
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
    editTodoItem() {
      this.editTodo(this.index);
    },
  },
};
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
}

.todo-text {
  flex-grow: 1;
}

.completed {
  text-decoration: line-through;
}

.delete-button {
  padding: 5px 10px;
  font-size: 14px;
  background-color: #dc3545;
  color: #fff;
  border: none;
  border-radius: 2px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #c82333;
}

.edit-button {
  padding: 5px 10px;
  font-size: 14px;
  background-color: #3543dc;
  color: #fff;
  border: none;
  border-radius: 2px;
  cursor: pointer;
  margin-left: 5px;
}

.edit-button:hover {
  background-color: #2e23c8;
}
</style>
