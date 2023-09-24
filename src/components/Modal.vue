<script setup>
import { ref } from "vue";
import Alerta from "./Alerta.vue";
import cerrarModal from "../assets/img/cerrar.svg";

const error = ref('');
const emit = defineEmits(['cerrar-modal', 'guardar-gasto', 'update:nombre', 'update:cantidad', 'update:categoria']);
const props = defineProps({
    modal: {
        type: Object,
        required: true
    },
    nombre: {
        type: String,
        required: true
    },
    cantidad: {
        type: [String, Number],
        required: true
    },
    categoria: {
        type: String,
        required: true
    },
    disponible: {
        type: Number,
        required: true
    }
})

const agregarGasto = () => {
    // Validar campos vacios
    const { cantidad, categoria, nombre, disponible } = props;
    if ([nombre, cantidad, categoria].includes('')) {
        error.value = "Todos los campos son obligatorios";
        return;
    }
    // Validar la cantidad
    if (cantidad <= 0) {
        error.value = "Ingresa una cantidad valida";
        return;
    }

    if (cantidad > disponible) {
        error.value = "Has excedido el prespuesto disponible";
        return;
    }
    emit('guardar-gasto');
}
</script>

<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img :src="cerrarModal" alt="cerrar modal" @click="$emit('cerrar-modal')" />
        </div>

        <div class="contenedor contenedor-formulario" :class="[modal.animar ? 'animar' : 'cerrar']">
            <form class="nuevo-gasto" @submit.prevent="agregarGasto">
                <legend>Agregar Gasto</legend>

                <Alerta v-if="error">
                    <template v-slot:header>Atención</template>
                    <template v-slot:contenido>{{ error }}</template>
                </Alerta>
                <div class="campo">
                    <label for="nombre">Nombre del gasto:</label>
                    <input type="text" name="nombre" id="nombre" placeholder="Agrega el nombre del gasto" :value="nombre"
                        @input="$emit('update:nombre', $event.target.value)">
                </div>
                <div class="campo">
                    <label for="cantidad">Cantidad:</label>
                    <input type="number" name="cantidad" id="cantidad" placeholder="Agrega la cantidad del gasto, ejemplo 300"
                        :value="cantidad" @input="$emit('update:cantidad', +$event.target.value)">
                </div>
                <div class="campo">
                    <label for="categoria">Categoria:</label>
                    <select id="categoria" :value="categoria" @input="$emit('update:categoria', $event.target.value)">
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
