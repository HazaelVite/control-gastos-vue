<script setup>
import { ref, reactive } from 'vue';
import Presupuesto from './components/Presupuesto.vue';
import ControlPresupues from './components/ControlPresupues.vue';
import Gasto from './components/Gasto.vue';
import Modal from './components/Modal.vue';
import icoNuevoGasto from "./assets/img/nuevo-gasto.svg";
import { generarId } from "./helpers"

const modal = reactive({
  mostrar: false,
  animar: false
})
const presupuesto = ref(0);
const disponible = ref(0);
const gasto = reactive({
  nombre: '',
  cantidad: '',
  categoria: '',
  id: null,
  fecha: Date.now()
})
const gastos = ref([]);

const colocarPresupuesto = (cantidad) => {
  presupuesto.value = cantidad
  disponible.value = cantidad
}

const mostrarModal = () => {
  setTimeout(() => {
    modal.animar = true;
  }, 300);

  modal.mostrar = true;
}

const cerrarModal = () => {
  modal.animar = false;
  setTimeout(() => {
    modal.mostrar = false;
  }, 300);
}

const guardarGasto = () => {
  gastos.value.push({
    ...gasto,
    id: generarId(),
  })
  // Ocultar el modal
  cerrarModal();
  Object.assign(gasto, {
    nombre: '',
    cantidad: '',
    categoria: '',
    id: null,
    fecha: Date.now()
  })
}
</script>

<template>
  <div :class="{fijar: modal.mostrar}">
  <header>
    <h1>Planificador de Gastos</h1>
    <div class="contenedor-header contenedor sombra">
      <Presupuesto v-if="presupuesto === 0" @colocar-presupuesto="colocarPresupuesto" />
      <ControlPresupues v-else :presupuesto="presupuesto" :disponible="disponible" />
    </div>
  </header>
  <main v-if="presupuesto > 0">
    <div class="listado-gastos contenedor">
      <h2>{{ gastos.length > 0 ? 'Gastos' : 'No hay gastos' }}</h2>
      <Gasto v-for="gasto in gastos" :key="gasto.id" :gasto="gasto" />
    </div>
    <div class="crear-gasto">
      <img :src="icoNuevoGasto" alt="Nuevo Gasto" @click="mostrarModal" />
    </div>
    <Modal v-if="modal.mostrar" @cerrar-modal="cerrarModal" @guardar-gasto="guardarGasto" :modal="modal"
      v-model:nombre="gasto.nombre" v-model:cantidad="gasto.cantidad" v-model:categoria="gasto.categoria" />
  </main>
</div>
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

.listado-gastos {
  margin-top: 10rem;
}

.listado-gastos h2 {
  color: var(--gris-oscuro);
  font-weight: 900;
}

.fijar {
  overflow: hidden;
  height: 100vh;
}
</style>
