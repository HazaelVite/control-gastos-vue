<script setup>
import { ref } from 'vue';
import Presupuesto from './components/Presupuesto.vue';
import ControlPresupues from './components/ControlPresupues.vue';
import icoNuevoGasto from "./assets/img/nuevo-gasto.svg";

const presupuesto = ref(0);
const disponible = ref(0);

const colocarPresupuesto = (cantidad) => {
  presupuesto.value = cantidad
  disponible.value = cantidad
}

</script>

<template>
  <header>
    <h1>Planificador de Gastos</h1>
    <div class="contenedor-header contenedor sombra">
      <Presupuesto v-if="presupuesto === 0" @colocar-presupuesto="colocarPresupuesto" />
      <ControlPresupues v-else :presupuesto="presupuesto" :disponible="disponible" />
    </div>
  </header>
  <main v-if="presupuesto > 0">
    <div class="crear-gasto">
      <img :src="icoNuevoGasto" alt="Nuevo Gasto" />
    </div>
  </main>
</template>

<style>
:root {
  --azul: #5f16be;
  --blanco: #fff;
  --gris-claro: #F5F5F5;
  --gris: #94A3B8;
  --gris-oscuro: #64748B;
  --negro: #202020;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: inherit;
}

body {
  font-size: 1.6rem;
  font-family: 'Lato', Tahoma, Geneva, Verdana, sans-serif;
  background-color: var(--gris-claro);
}

h1 {
  font-size: 4rem;
}

h2 {
  font-size: 3rem;
}

header {
  /* background-color: var(--azul); */
  background-image: url('https://w.wallhaven.cc/full/ex/wallhaven-ex9gwo.png');
  background-position: center center;
}

header h1 {
  padding: 3rem 0;
  margin: 0;
  color: var(--blanco);
  text-align: center;
}

.contenedor {
  width: 90%;
  max-width: 80rem;
  margin: 0 auto;
}

.sombra {
  box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
  background-color: var(--blanco);
  border-radius: 1rem;
  padding: 5rem;
}

.contenedor-header {
  margin-top: -5rem;
  transform: translateY(5rem);
  padding: 5rem;
}

.crear-gasto {
    position: fixed;
    bottom: 5rem;
    right: 5rem;
}

.crear-gasto img {
    width: 5rem;
    cursor: pointer;
}
</style>
