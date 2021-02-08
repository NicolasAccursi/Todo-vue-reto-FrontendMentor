<template>
  <h1>ToDos</h1>
  <TodoForm />
</template>

<script>
import { provide, ref } from "vue";
import TodoForm from "./TodoForm.vue";
export default {
  components: { TodoForm },
  setup() {
    const todos = ref([]);
    provide("todos", todos);
  },
};
</script>

<style></style>
