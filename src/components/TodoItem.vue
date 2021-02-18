<template>
  <li
    class="itemdrag ModoColor list-group-item d-flex justify-content-between align-items-center"
  >
    <span
      :class="{ tachado: todo.estado }"
      role="button"
      @click="completado(todo.id)"
    >
      <i
        class="circulo me-3"
        :class="todo.estado ? 'fas fa-check-circle' : 'far fa-circle'"
      ></i>
      <span>{{ todo.texto }}</span></span
    >

    <span role="button" @click="eliminar(todo.id)">
      <i class="fas fa-times"></i>
    </span>
  </li>
</template>

<script>
import { inject } from "vue";
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const todos = inject("todos");

    const eliminar = (id) => {
      todos.value = todos.value.filter((item) => item.id !== id);
    };

    const completado = (id) => {
      todos.value = todos.value.map((item) => {
        if (item.id === id) {
          item.estado = !item.estado;
        }
        return item;
      });
    };

    return { eliminar, completado };
  },
};
</script>

<style>
span {
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.tachado {
  text-decoration: line-through;
}

span:hover > .circulo,
.circulo {
  font-size: 22px;
  background: var(--Check-Background);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.fa-circle {
  background: hsl(0, 0%, 98%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
