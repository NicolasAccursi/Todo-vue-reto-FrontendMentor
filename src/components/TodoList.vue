<template>
  <draggable
    tag="ul"
    class="list-group"
    draggable=".itemdrag"
    :animation="100"
    @start="dragging = true"
    @end="dragging = false"
    :list="todos"
  >
    <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    <li v-if="todos.length === 0" class="list-group-item ModoColor">
      No hay ToDos
    </li>
    <TodoFooter v-if="todos.length !== 0 || estado === 'completados'" />
  </draggable>
  <TodoFiltro v-if="mobile" />
</template>

<script>
import { computed, inject, provide, ref } from "vue";
import TodoItem from "./TodoItem.vue";
import TodoFooter from "./TodoFooter.vue";
import TodoFiltro from "./TodoFiltro.vue";
import { VueDraggableNext } from "vue-draggable-next";
export default {
  components: { TodoItem, TodoFooter, TodoFiltro, draggable: VueDraggableNext },
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
    return { todos, mobile, estado };
  },
};
</script>

<style></style>
