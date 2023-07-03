<script setup>
import Presupuesto from './Presupuesto.vue';
</script>

<template>
    <header>
        <h1>Planificador de Gastos</h1>
        <div class="contenedor-header contenedor sombra">
            <Presupuesto /> 
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
