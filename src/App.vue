<template>
  <div id="app">
    <TodoBoard :todos="todos" :addTodo="addTodo" :deleteTodo="deleteTodo" :editTodo="editTodo" :changeStatusTodo="changeStatusTodo" />
    
    <div v-if="isEditing" class="modal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <input type="text" v-model="editedTodo.text">
        <div class="buttons">
          <button class="save" @click="saveEdit">Save</button>
        </div>
      </div>
    </div>
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
      isEditing: false,
      editedTodo: {
        index: null,
        text: ''
      }
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index) {
      this.editedTodo.index = index;
      this.editedTodo.text = this.todos[index].text;
      this.isEditing = true;
    },
    saveEdit() {
      this.todos[this.editedTodo.index].text = this.editedTodo.text;
      this.isEditing = false;
    },
    closeModal() {
      this.isEditing = false;
    },
    changeStatusTodo(index) {
      this.todos[index].completed = !this.todos[index].completed;
    },
  },
};
</script>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center; 
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.4);
}

.modal-content {
  background-color: #ffffff;
  padding: 20px;
  border: 1px solid #888;
  max-width: 400px; 
}

.close {
  color: #000000;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.buttons {
  display: flex;
  justify-content: flex-end;
}

.save {
  color: #ffffff;
  background-color: chartreuse;
  padding: 5px 10px;
  font-size: 14px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: rgb(0, 0, 0);
  text-decoration: none;
  cursor: pointer;
}
</style>
