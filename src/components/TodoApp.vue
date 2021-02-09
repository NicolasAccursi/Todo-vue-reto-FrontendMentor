<template>
  <div :class="{ Dark: !light }">
    <img
      v-bind:src="light ? ImgL : ImgD"
      class="img-fluid"
      alt="Responsive image"
    />
    <div class="mt-5 d-flex justify-content-between align-items-center ">
      <h1>TODO</h1>
      <span role="button" @click="cambiaModo">
        <i id="IconoModo" :class="light ? 'fas fa-moon' : 'fas fa-sun'"></i
      ></span>
    </div>
    <TodoForm />
    <TodoList />
  </div>
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
export default {
  components: { TodoForm, TodoList },
  setup() {
    const todos = ref([]);
    const light = ref(true);
    const ImgL = require("../assets/images/bg-desktop-light.jpg");
    const ImgD = require("../assets/images/bg-desktop-dark.jpg");

    provide("todos", todos);
    provide("light", light);

    const cambiaModo = () => {
      if (light.value) document.body.className = "bodyDark";
      else document.body.className = "";

      light.value = !light.value;
    };

    if (localStorage.getItem("todos")) {
      todos.value = JSON.parse(localStorage.getItem("todos"));
    }
    watchEffect(() => {
      localStorage.setItem("todos", JSON.stringify(todos.value));
    });

    return { todos, light, cambiaModo, ImgL, ImgD };
  },
};
</script>

<style>
.Dark .ModoColor {
  background: var(--Very-Dark-DesaturatedBlue);
  color: var(--Light-Grayish-Blue);
}
.bodyDark {
  background: var(--Very-Dark-Blue);
}

h1 {
  font-weight: 700;
  color: hsl(0, 0%, 98%);
  letter-spacing: 8px;
}

#IconoModo {
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  font-size: 20px;
  color: hsl(0, 0%, 98%);
}

img {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -10;
  width: 100%;
  min-height: 200px;
}
</style>
