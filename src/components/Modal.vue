<script setup>
import cerrarModal from "../assets/img/cerrar.svg";

const emit = defineEmits(['cerrar-modal'])
</script>

<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img :src="cerrarModal" alt="cerrar modal" @click="$emit('cerrar-modal')" />
        </div>

        <div class="contenedor">
            <form>
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
                        <option value="">-- Seleccioanr --</option>
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
</style>
