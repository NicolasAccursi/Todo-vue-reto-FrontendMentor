<template>
  <li
    class="ModoColor list-group-item d-flex justify-content-between align-items-center"
  >
    <todo-item-activo v-slot="slotProps">
      {{ slotProps.activos }} Activos
    </todo-item-activo>

    <span role="button"> {{ contarActivos }} Activos</span>
    <span role="button" @click="eliminarCompletados">
      Eliminar Completados
    </span>
  </li>
</template>

<script>
import TodoItemActivo from "./TodoItemActivo.vue";

export default {
  components: { TodoItemActivo },
};
</script>
