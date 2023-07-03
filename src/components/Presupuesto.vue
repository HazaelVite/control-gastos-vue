<script setup>
 import { ref } from 'vue';
 import Alerta from './Alerta.vue';
 const presupuesto = ref(0);
 const isError = ref(false);

 const definirPresupuesto = () => {
    if (presupuesto.value <= 0) {
        isError.value = true;
        setTimeout(() => {
            isError.value = false;
        }, 3000)
    }
 }
</script>

<template>
    <form
    class="presupuesto"
    @submit.prevent="definirPresupuesto"
    >
        <div class="campo">
            <label for="preuspuesto">Definir presupuesto</label>
            <input 
            type="number" 
            id="presupuesto" 
            min="0" 
            placeholder="Presupuesto"
            v-model.number="presupuesto"
            />
        </div>
        <Alerta v-if="isError">
            <template v-slot:header>Error</template>
            <template v-slot:contenido>Por favor, ingresa un presupuesto mayor a cero</template>
        </Alerta>
        <input type="submit" value="Definir Presupuesto" :disabled="isError" />
    </form>
</template>

<style scoped>
.presupuesto {
    width: 100%;
}
.campo {
    display: grid;
    gap: 2rem;
}
.presupuesto label {
    font-size: 2.2rem;
    text-align: center;
    font-weight: 700;
    color: var(--azul);
}
.presupuesto input[type="number"] {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
    text-align: center;
}
.presupuesto input[type="submit"] {
    background-color: var(--azul);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2rem;
    text-align: center;
    margin-top: 2rem;
    color: var(--blanco);
    font-weight: 900;
    width: 100%;
    transition: backgroud-color 300ms ease;
}
.presupuesto input[type="submit"]:hover {
    background-color: #4910a4;
    cursor: pointer;
}
.presupuesto input[type="submit"]:disabled {
    background-color: var(--gris-claro);
    color: var(--gris-oscuro);
    cursor: default;
}
</style>
