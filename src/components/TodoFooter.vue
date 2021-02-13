<template>
  <li
    class="item ModoColor list-group-item d-flex justify-content-between align-items-center"
  >
    <span role="button" class="pe-3"> {{ contarActivos }} Activos</span>
    <todoFiltroOpciones v-if="!mobile" />
    <span role="button" class="ps-3" @click="eliminarCompletados">
      Limpiar completos
    </span>
  </li>
</template>

<script>
import { computed, inject } from "vue";
import todoFiltroOpciones from "./todoFiltroOpciones.vue";
export default {
  components: { todoFiltroOpciones },
  setup() {
    const todos = inject("todos");
    const mobile = inject("mobile");
    const contarActivos = computed(() => {
      return todos.value.filter((item) => item.estado === false).length;
    });
    const eliminarCompletados = () => {
      todos.value = todos.value.filter((item) => item.estado === false);
    };

    return { contarActivos, eliminarCompletados, mobile, todos };
  },
};
</script>
<style scoped>
* {
  font-size: 12px;
  font-weight: 400;
}
.item {
  color: var(--Dark-Grayish-Blue);
}
.item span:hover {
  color: var(--Very-Dark-GrayishBlue);
}
</style>
