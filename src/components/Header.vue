<script setup>
import { ref } from 'vue';
import Presupuesto from './Presupuesto.vue';

const presupuesto = ref(0)

const colocarPresupuesto = (cantidad) => {
    presupuesto.value = cantidad
}

</script>

<template>
    <header>
        <h1>Planificador de Gastos</h1>
        <div class="contenedor-header contenedor sombra">
            <Presupuesto v-if="presupuesto === 0" @colocar-presupuesto="colocarPresupuesto" />
            <div v-else>{{ presupuesto }}</div>
        </div>
    </header>
</template>

<style scoped>
.contenedor-header {
    margin-top: -5rem;
    transform: translateY(5rem);
    padding: 5rem;
}
</style>
