<template>
  <ul class="list-group">
    <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    <li v-if="todos.length === 0" class="list-group-item">
      No hay ToDos...
    </li>
    <TodoFooter v-if="todos.length !== 0" />
    <todo-filtro />
  </ul>
</template>

<script>
import { computed, inject, provide, ref } from "vue";
import TodoItem from "./TodoItem.vue";
import TodoFooter from "./TodoFooter.vue";
import TodoFiltro from "./TodoFiltro.vue";

export default {
  components: { TodoItem, TodoFooter, TodoFiltro },
  setup() {
    const todosTodos = inject("todos");

    const estado = ref("all");

    const todos = computed(() => {
      if (estado.value === "all") {
        return todosTodos.value;
      }
      if (estado.value === "active") {
        return todosTodos.value.filter(item => item.estado === false);
      }
      if (estado.value === "complete") {
        return todosTodos.value.filter(item => item.estado === true);
      }
    });

    provide("estado", estado);

    return { todos };
  }
};
</script>
