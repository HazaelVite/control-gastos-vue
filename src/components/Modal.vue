<script setup>
import cerrarModal from "../assets/img/cerrar.svg";

const emit = defineEmits(['cerrar-modal']);
const props = defineProps({
    modal: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img :src="cerrarModal" alt="cerrar modal" @click="$emit('cerrar-modal')" />
        </div>

        <div class="contenedor contenedor-formulario" :class="[modal.animar ? 'animar' : 'cerrar']">
            <form class="nuevo-gasto">
                <legend>Agregar Gasto</legend>
                <div class="campo">
                    <label for="nombre">Nombre del gasto:</label>
                    <input type="text" name="nombre" id="nombre" placeholder="Agrega el nombre del gasto">
                </div>
                <div class="campo">
                    <label for="cantidad">Cantidad:</label>
                    <input type="text" name="cantidad" id="cantidad" placeholder="Agrega la cantidad del gasto, ejemplo 300">
                </div>
                <div class="campo">
                    <label for="categoria">Categoria:</label>
                    <select id="categoria">
                        <option value="">-- Seleccionar --</option>
                        <option value="ahorro">Ahorro</option>
                        <option value="comida">Comida</option>
                        <option value="casa">Casa</option>
                        <option value="varios">Gastos Varios</option>
                        <option value="ocio">Ocio</option>
                        <option value="salud">Salud</option>
                        <option value="suscripciones">Suscripciones</option>
                    </select>
                </div>
                <input type="submit" value="Agregar gasto" class="" />
            </form>
        </div>
    </div>
</template>

<style scoped>
.modal {
    position: absolute;
    background-color: rgb(0 0 0 / 0.8);
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

.cerrar-modal {
    position: absolute;
    right: 3rem;
    top: 3rem;
}

.cerrar-modal img {
    width: 3rem;
    cursor: pointer;
}

.contenedor-formulario {
    transition-property: all;
    transition-duration: 300ms;
    transition-timing-function: ease-in;
    opacity: 0;
}

.contenedor-formulario.animar {
    opacity: 1;
}

.contenedor-formulario.cerrar {
    opacity: 0;
}

.nuevo-gasto {
    margin: 10rem auto 0 auto;
    display: grid;
    gap: 2rem;
}
.campo {
    display: grid;
    gap: 2rem;
}
.nuevo-gasto legend {
    text-align: center;
    color: var(--blanco);
    font-size: 3rem;
    font-weight: 700;
}
.nuevo-gasto input,
.nuevo-gasto select {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
}
.nuevo-gasto label {
    color: var(--blanco);
    font-size: 3rem;
}
.nuevo-gasto input[type="submit"] {
    background-color: var(--azul);
    color: var(--blanco);
    font-weight: 700;
    cursor: pointer;
}
</style>
