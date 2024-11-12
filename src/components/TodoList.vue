<template>
  <div class="todo-list-container">
    <ul>
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <!-- チェックボックスで完了状態を切り替える -->
        <input
          type="checkbox"
          v-model="todo.completed"
          @change="toggleCompleted(todo.id)"
        />

        <!-- 完了したTodoに打ち消し線を追加 -->
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <!-- 削除ボタン -->
        <button @click="removeTodo(todo.id)" class="remove-button">削除</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  todos: Array,
});

const emit = defineEmits(["removeTodo"]);

const removeTodo = (id) => {
  emit("removeTodo", id);
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}

.todo-list-container {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}

ul {
  list-style-type: none;
  padding: 0;
  width: 300px;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.todo-item span {
  font-size: 1.1rem;
}

.remove-button {
  background-color: #e57373;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

.remove-button:hover {
  background-color: #ef5350;
}
</style>
