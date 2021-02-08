<template>
  <form @submit.prevent="formulario">
    <input
      type="text"
      class="form-control my-3"
      placeholder="Ingrese tarea"
      v-model="texto"
    />
  </form>
</template>

<script>
import { inject, ref } from "vue";
export default {
  setup() {
    const todos = inject("todos");

    const texto = ref("");

    const formulario = () => {
      console.log(texto.value);
    };
    return { formulario, texto };
  },
};
</script>

<style></style>
