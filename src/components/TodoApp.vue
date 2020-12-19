<template>
  <h1>ToDos</h1>
  <TodoForm />
  <TodoList />
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";

export default {
  name: "TodoApp",
  components: {
    TodoForm,
    TodoList
  },
  setup() {
    const todos = ref([]);
    provide("todos", todos);

    if (localStorage.getItem("todos")) {
      todos.value = JSON.parse(localStorage.getItem("todos"));
    }

    watchEffect(() => {
      // console.log(todos.value.length);
      // console.log(todos.value);
      localStorage.setItem("todos", JSON.stringify(todos.value));
    });
  }
};
</script>
