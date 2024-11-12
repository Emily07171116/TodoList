<template>
  <div class="todo-input-container">
    <input
      v-model="newTodo"
      @keyup.enter="addTodo"
      type="text"
      placeholder="新しいTodoを追加"
      class="todo-input"
    />
    <button @click="addTodo" class="add-button">追加</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newTodo = ref("");
const emit = defineEmits(["addTodo"]);

const addTodo = () => {
  if (newTodo.value.trim() !== "") {
    const todo = {
      id: Date.now(),
      text: newTodo.value,
    };
    emit("addTodo", todo);
    newTodo.value = "";
  }
};
</script>

<style scoped>
.todo-input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 20px;
}

.todo-input {
  padding: 10px;
  font-size: 1rem;
  border-radius: 5px;
  border: 1px solid #ddd;
  width: 250px;
  box-sizing: border-box;
}

.todo-input:focus {
  outline: none;
  border-color: #5c6bc0;
}

.add-button {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #5c6bc0;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.add-button:hover {
  background-color: #3f4f8c;
}
</style>
