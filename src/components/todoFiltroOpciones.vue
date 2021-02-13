<template>
  <div class="card-body d-flex justify-content-between align-items-center">
    <span
      :class="{ 'active-item': activo('activos') }"
      role="button"
      @click="cambioEstado('activos')"
      >Activos</span
    >
    <span
      :class="{ 'active-item': activo('all') }"
      role="button"
      @click="cambioEstado('all')"
      >Todos</span
    >
    <span
      :class="{ 'active-item': activo('completados') }"
      role="button"
      @click="cambioEstado('completados')"
      >Completos</span
    >
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

    const activo = (valor) => valor === estado.value;

    return { cambioEstado, activo };
  },
};
</script>

<style scoped>
.active-item {
  color: var(--Bright-Blue);
  font-weight: 700;
}

.item span:not(.active-item):hover {
  color: var(--Very-Dark-GrayishBlue);
}
</style>
