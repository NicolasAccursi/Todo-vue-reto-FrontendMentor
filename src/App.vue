<template>
  <div class="container"><TodoApp /></div>
</template>

<script>
import TodoApp from "./components/TodoApp.vue";

export default {
  components: { TodoApp },
  name: "App",
};
</script>

<style>
:root {
  --Bright-Blue: hsl(220, 98%, 61%);
  --Check-Background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(hsl(192, 100%, 67%)),
    to(hsl(280, 87%, 65%))
  );

  --Very-Light-Gray: hsl(0, 0%, 98%);
  --Very-Light-GrayishBlue: hsl(236, 33%, 92%);
  --Light-Grayish-Blue: hsl(233, 11%, 84%);
  --Dark-Grayish-Blue: hsl(236, 9%, 61%);
  --Very-Dark-GrayishBlue: hsl(235, 19%, 35%);

  --Very-Dark-Blue: hsl(235, 21%, 11%);
  --Very-Dark-DesaturatedBlue: hsl(235, 24%, 19%);
  --Light-Grayish-Blue: hsl(234, 39%, 85%);
  --Light-Grayish-Blue-hover: hsl(236, 33%, 92%);
  --Dark-Grayish-Blue: hsl(234, 11%, 52%);
  --Very-Dark-Grayish-Blue: hsl(233, 14%, 35%);
  --Very-Dark-Grayish-Blue-hover: hsl(237, 14%, 26%);
}

body {
  font-family: "Josefin Sans", sans-serif;
  font-size: 18px;
}

.container {
  max-width: 450px;
}
</style>
