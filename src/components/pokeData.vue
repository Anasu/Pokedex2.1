<template>
    <h2 class="respuesta__nombre">#{{ pokeID }} - {{ pokeName }}</h2>
</template>

<script>
export default {
    props: {
        pokeName: {
            type: String,
            required: false,
            default() {
                return 'No se encontró el pokemon';
            }
        },
        pokeID: {
            type: Number,
            required: false,
            default() {
                return 0;
            }
        }
    }
}
</script>

<style>
    .respuesta__nombre{
    text-transform: capitalize;
    }
</style>