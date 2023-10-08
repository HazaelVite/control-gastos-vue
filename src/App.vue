<script setup>
import { ref, reactive, watch, computed } from "vue";
import Presupuesto from "./components/Presupuesto.vue";
import ControlPresupues from "./components/ControlPresupues.vue";
import Gasto from "./components/Gasto.vue";
import Modal from "./components/Modal.vue";
import Filtros from "./components/Filtros.vue";
import icoNuevoGasto from "./assets/img/nuevo-gasto.svg";
import { generarId } from "./helpers";

const modal = reactive({
  mostrar: false,
  animar: false,
});
const presupuesto = ref(0);
const disponible = ref(0);
const gastado = ref(0);
const filtro = ref('');

const gasto = reactive({
  nombre: "",
  cantidad: "",
  categoria: "",
  id: null,
  fecha: Date.now(),
});
const gastos = ref([]);

// Watch
watch(
  gastos,
  () => {
    const totalGastado = gastos.value.reduce(
      (total, gasto) => gasto.cantidad + total,
      0
    );
    gastado.value = totalGastado;
    disponible.value = presupuesto.value - totalGastado;
  },
  { deep: true }
);

watch(
  modal,
  () => {
    if (!modal.mostrar) {
      reiniciarFormulario();
    }
  },
  { deep: true }
);

const colocarPresupuesto = (cantidad) => {
  presupuesto.value = cantidad;
  disponible.value = cantidad;
};

const mostrarModal = () => {
  setTimeout(() => {
    modal.animar = true;
  }, 300);

  modal.mostrar = true;
};

const cerrarModal = () => {
  modal.animar = false;
  setTimeout(() => {
    modal.mostrar = false;
  }, 300);
};

const guardarGasto = () => {
  if (gasto.id) {
    // Editando...
    const { id } = gasto;
    const idx = gastos.value.findIndex((gasto => gasto.id === id));
    gastos.value[idx] = {...gasto};
  } else {
    gastos.value.push({
      ...gasto,
      id: generarId(),
    });
  }
  // Ocultar el modal
  cerrarModal();
  reiniciarFormulario();
};

const reiniciarFormulario = () => {
  Object.assign(gasto, {
    nombre: "",
    cantidad: "",
    categoria: "",
    id: null,
    fecha: Date.now(),
  });
};

const seleccionarGasto = (id) => {
  const gastoEditar = gastos.value.filter((gasto) => gasto.id === id)[0];
  Object.assign(gasto, gastoEditar);
  mostrarModal();
};

const eliminarGasto = (id) => {
  if(confirm('Seguro que deseas eliminar este gasto?')) {
    gastos.value = gastos.value.filter(gastoState => gastoState.id !== gasto.id);
    cerrarModal();
  }
}

const gastosFiltrados = computed(() => {
  if(filtro.value) {
    return gastos.value.filter(gasto => gasto.categoria === filtro.value)
  }
  return gastos.value;
})
</script>

<template>
  <div :class="{ fijar: modal.mostrar }">
    <header>
      <h1>Planificador de Gastos</h1>
      <div class="contenedor-header contenedor sombra">
        <Presupuesto
          v-if="presupuesto === 0"
          @colocar-presupuesto="colocarPresupuesto"
        />
        <ControlPresupues
          v-else
          :presupuesto="presupuesto"
          :disponible="disponible"
          :gastado="gastado"
        />
      </div>
    </header>
    <main v-if="presupuesto > 0">
      <Filtros
        v-model:filtro="filtro"
      />
      <div class="listado-gastos contenedor">
        <h2>{{ gastosFiltrados.length > 0 ? "Gastos" : "No hay gastos" }}</h2>
        <Gasto
          v-for="gasto in gastosFiltrados"
          :key="gasto.id"
          :gasto="gasto"
          @seleccionar-gasto="seleccionarGasto"
        />
      </div>
      <div class="crear-gasto">
        <img :src="icoNuevoGasto" alt="Nuevo Gasto" @click="mostrarModal" />
      </div>
      <Modal
        v-if="modal.mostrar"
        @cerrar-modal="cerrarModal"
        @guardar-gasto="guardarGasto"
        @eliminar-gasto="eliminarGasto"
        :modal="modal"
        :id="gasto.id"
        :disponible="disponible"
        v-model:nombre="gasto.nombre"
        v-model:cantidad="gasto.cantidad"
        v-model:categoria="gasto.categoria"
      />
    </main>
  </div>
</template>

<style>
:root {
  --azul: #5f16be;
  --blanco: #fff;
  --gris-claro: #f5f5f5;
  --gris: #94a3b8;
  --gris-oscuro: #64748b;
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
  font-family: "Lato", Tahoma, Geneva, Verdana, sans-serif;
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
  background-image: url("https://w.wallhaven.cc/full/ex/wallhaven-ex9gwo.png");
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
