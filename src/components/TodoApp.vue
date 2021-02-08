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
  components: { TodoForm, TodoList },
  setup() {
    const todos = ref([]);
    provide("todos", todos);

    if (localStorage.getItem("todos")) {
      todos.value = JSON.parse(localStorage.getItem("todos"));
    }
    watchEffect(() => {
      localStorage.setItem("todos", JSON.stringify(todos.value));
    });

    return { todos };
  },
};
</script>

<style></style>
