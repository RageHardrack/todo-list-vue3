<template>
  <form @submit.prevent="agregarTarea">
    <input
      type="text"
      class="form-control my-3"
      placeholder="Ingrese tarea"
      v-model.trim="texto"
    />
  </form>
</template>

<script>
import { inject, ref } from "vue";
export default {
  setup() {
    const todos = inject("todos");
    const texto = ref("");

    const agregarTarea = () => {
      //   console.log(texto.value);
      if (texto.value === "") {
        console.log("Está vacío");
        return;
      }
      const todo = {
        texto: texto.value,
        estado: false,
        id: Date.now()
      };

      todos.value.push(todo);
      console.log(todos.value);

      texto.value = "";
      // console.log(todo);
    };

    return { agregarTarea, texto };
  }
};
</script>
