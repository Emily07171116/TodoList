<template>
  <li>
    <input type="checkbox" v-model="todo.completed" @change="toggleCompleted" />
    <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
    <button @click="removeTodo">削除</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: Object,
    index: Number,
  },
  setup(props, { emit }) {
    const toggleCompleted = () => {
      emit("toggle-completed", props.index);
    };

    const removeTodo = () => {
      emit("remove-todo", props.index);
    };

    return {
      toggleCompleted,
      removeTodo,
    };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
