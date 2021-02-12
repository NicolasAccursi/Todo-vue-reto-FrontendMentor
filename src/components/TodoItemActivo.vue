<template>
  <span role="button"><slot v-bind:activos="contarActivos"/></span>
</template>

<script>
import { computed, inject } from "vue";
export default {
  setup() {
    const todos = inject("todos");

    const contarActivos = computed(() => {
      return todos.value.filter((item) => item.estado === false).length;
    });
    const eliminarCompletados = () => {
      todos.value = todos.value.filter((item) => item.estado === false);
    };

    return { contarActivos, eliminarCompletados };
  },
};
</script>

<style></style>
