<script setup>
const props = defineProps({

    alerta: {
        type: Object,
        required: true,

    }
})
</script>

<template>
    <div>
        {{ alerta.mensaje }}
    </div>
</template>
