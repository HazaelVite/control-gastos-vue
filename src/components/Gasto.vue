<script setup>
import icoNuevoGasto from "../assets/img/nuevo-gasto.svg";
</script>

<template>
    <main>
        <div class="crear-gasto">
            <img :src="icoNuevoGasto" alt="Nuevo Gasto" />
        </div>
    </main>
</template>

<style scoped>
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
