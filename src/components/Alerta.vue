<script setup>
import { computed } from 'vue';

//y aqui recibo el estado como prop para poder utilizarloe en el componente
const props = defineProps({

    alerta: {
        type: Object,
        required: true,

    }
})

const isError = computed(() => {
    //acceder al valor del tipo de alerta y verificar si es error
    return props.alerta.tipo == 'error'
});
</script>

<template>
    <!--:class es para clases dinamicas -->
    <div 
    :class="[isError ? 'bg-red-500' : 'bg-green-500']"
    class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md">
        {{ alerta.mensaje }}
    </div>
</template>
