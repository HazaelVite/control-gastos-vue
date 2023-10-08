<script setup>
import CircleProgress from "vue3-circle-progress";
import "vue3-circle-progress/dist/circle-progress.css";
import { formatearCantidad } from "../helpers";

defineEmits(["reset-app"]);

const prosp = defineProps({
  presupuesto: {
    type: Number,
    required: true,
  },
  disponible: {
    type: Number,
    required: true,
  },
  gastado: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="dos-columnas">
    <div class="contenedor-grafico">
      <circle-progress
        :percent="10"
        :size="250"
        :border-width="25"
        :border-bg-width="25"
        :transition="2000"
        fill-color="#5f16be"
        empty-color="#F5F5F5"
      />
    </div>
    <div class="contenedor-presupuesto">
      <button class="reset-app" type="button" @click="$emit('reset-app')">
        Reiniciar App
      </button>
      <p>
        <span>Presupuesto:</span>
        {{ formatearCantidad(presupuesto) }}
      </p>
      <p>
        <span>Disponible:</span>
        {{ formatearCantidad(disponible) }}
      </p>
      <p>
        <span>Gastado:</span>
        {{ formatearCantidad(gastado) }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.dos-columnas {
  display: flex;
  flex-direction: column;
}

.dos-columnas > :first-child {
  margin-bottom: 3rem;
}

@media (min-width: 768px) {
  .dos-columnas {
    flex-direction: row;
    gap: 3rem;
    align-items: center;
  }

  .dos-columnas > :first-child {
    margin-bottom: 0;
  }
}
.contenedor-presupuesto {
  width: 100%;
}
.contenedor-presupuesto p {
  font-size: 2.4rem;
  text-align: center;
  color: var(--gris-oscuro);
}
@media (min-width: 768px) {
  .contenedor-presupuesto p {
    text-align: left;
  }
}
.contenedor-presupuesto span {
  font-weight: 900;
  color: var(--azul);
}
.reset-app {
  background-color: rgb(138, 47, 223);
  border: none;
  padding: 1rem;
  width: 100%;
  color: var(--blanco);
  font-weight: 900;
  text-transform: uppercase;
  border-radius: 1rem;
  transition-property: backgroud-color;
  transition-duration: 300ms;
}
.reset-app:hover {
  cursor: pointer;
  background-color: rgb(106, 34, 173);
}
</style>
