<template>
  <div :class="{ Dark: !light }">
    <img
      :src="
        require('../assets/images/bg-' +
          (mobile ? 'mobile' : 'desktop') +
          '-' +
          (light ? 'dark' : 'light') +
          '.jpg')
      "
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
    <small
      class="ModoColor mt-3 card-body d-flex justify-content-center align-items-center"
    >
      Arraste y suelte para ordenar la lista
    </small>
  </div>
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
import { useWindowSize } from "vue-window-size";
export default {
  components: { TodoForm, TodoList },
  setup() {
    const todos = ref([]);
    const light = ref(true);
    const mobile = ref();
    const { width, height } = useWindowSize();

    provide("todos", todos);
    provide("light", light);
    provide("mobile", mobile);

    const cambiaModo = () => {
      light.value = !light.value;
    };

    if (localStorage.getItem("todos")) {
      todos.value = JSON.parse(localStorage.getItem("todos"));
    }

    if (localStorage.getItem("modo")) {
      if (localStorage.getItem("modo") === "false") light.value = false;
    }

    watchEffect(() => {
      localStorage.setItem("todos", JSON.stringify(todos.value));
      localStorage.setItem("modo", light.value);

      if (width.value <= 700) {
        mobile.value = true;
      } else {
        mobile.value = false;
      }

      if (!light.value) document.body.className = "bodyDark";
      else document.body.className = "";
    });

    return { todos, light, cambiaModo, mobile };
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

small {
  color: var(--Dark-Grayish-Blue);
}
</style>
