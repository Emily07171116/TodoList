<template>
  <div class="app-container">
    <h1 class="title">Todo アプリ</h1>
    <!--
    新しいTodoを追加するコンポーネント
    @addTodo="addTodo"はaddTodoイベントを受け取った際にApp.vueのaddTodoメゾットを呼び出す。
    ""内がApp.vueのメゾット
    -->
    <TodoInput @addTodo="addTodo" />
    <!--Todoリストを表示するコンポーネント-->
    <TodoList
      :todos="todos"
      @removeTodo="removeTodo"
      @toggleCompleted="toggleCompleted"
    />
  </div>
</template>

<script setup>
import { watch, onMounted, ref } from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

//初期状態のTodoリストをローカルストレージから読み込む
const todos = ref([]);

//ローカルストレージからtodosを取得
const loadTodos = () => {
  const storedTodos = localStorage.getItem("todos");
  if (storedTodos) {
    todos.value = JSON.parse(storedTodos);
  }
};

//Todoが変わるたびにローカルストレージに保存
watch(
  todos,
  () => {
    localStorage.setItem("todos", JSON.stringify(todos.value));
  },
  { deep: true }
);

//コンポーネントがマウントされたときにローカルストレージからデータを読み込む
onMounted(loadTodos);

//新しいTodoを追加
const addTodo = (todo) => {
  todos.value.push(todo);
};

// Todoを削除
const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

// Todoの完了状態を切り替え
const toggleCompleted = (id) => {
  const todo = todos.value.find((todo) => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed; // 完了状態を反転
  }
};
</script>

<style>
.app-container {
  max-width: 400px;
  margin: 50px auto;
  background-color: #f7f7f7;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  font-size: 2rem;
  color: #5c6bc0;
  margin-bottom: 20px;
}
</style>
