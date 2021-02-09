<template>
  <div class="ModoColor card mt-3">
    <div class="card-body d-flex justify-content-between align-items-center">
      <span role="button" @click="cambioEstado('activos')">Activos</span>
      <span role="button" @click="cambioEstado('all')">Todos</span>
      <span role="button" @click="cambioEstado('completados')"
        >Completados</span
      >
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  setup() {
    const estado = inject("estado");

    const cambioEstado = (valor) => {
      estado.value = valor;
    };

    return { cambioEstado };
  },
};
</script>

<style></style>
