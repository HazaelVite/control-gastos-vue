<script setup>

</script>

<template>
    <div class="alerta">
        <slot name="header"></slot>
        <hr>
        <slot name="contenido"></slot>
    </div>
</template>

<style>
.alerta {
    padding: 1rem;
    font-weight: 900;
    font-size: 1.6rem;
    text-transform: uppercase;
    text-align: center;
    background-color: var(--blanco);
    border-left: .5rem solid #B91C1C;
    color: #B91C1C;
    margin-top: 2rem;
}
</style>
