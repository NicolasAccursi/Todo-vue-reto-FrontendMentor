<template>
  <ul class="list-group">
    <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    <TodoFooter v-if="todos.length !== 0" />
    <li v-if="todos.length === 0 && !mobile" class="list-group-item">
      No hay ToDos
    </li>
  </ul>
  <TodoFiltro v-if="mobile" />
</template>

<script>
import { computed, inject, provide, ref } from "vue";
import TodoItem from "./TodoItem.vue";
import TodoFooter from "./TodoFooter.vue";
import TodoFiltro from "./TodoFiltro.vue";
export default {
  components: { TodoItem, TodoFooter, TodoFiltro },
  setup() {
    const todosOriginal = inject("todos");
    const mobile = inject("mobile");

    const estado = ref("all");

    const todos = computed(() => {
      if (estado.value === "all") {
        return todosOriginal.value;
      }

      if (estado.value === "activos") {
        return todosOriginal.value.filter((item) => item.estado === false);
      }

      if (estado.value === "completados") {
        return todosOriginal.value.filter((item) => item.estado === true);
      }
    });

    provide("estado", estado);
    return { todos, mobile };
  },
};
</script>

<style></style>
