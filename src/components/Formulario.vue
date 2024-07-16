<script setup>
import { reactive, computed} from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    tipo: '',
    mensaje: ''
})



const emit = defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente'])
const props = defineProps({
    id: {
        type: [String, null],
        required: true
    },
    nombre: {
        type: String,
        required: true
    },
    propietario: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    alta: {
        type: String,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    }

})

const validar = () => {
    if (Object.values(props).includes('')) {
        alerta.mensaje = "Todos los campos son obligarorios"
        alerta.tipo = "error"
        return
    }
    emit('guardar-paciente');
    alerta.mensaje = 'Paciente Agregado Exitosamente'
    alerta.tipo = 'success'
    setTimeout(() => {
        Object.assign(alerta, {
            tipo: '',
            mensaje: '',
        })
    }, 3000)
}
const editando = computed(() => {
    return props.id
});
</script>

<template>
    <div class="md:1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>

        <!--Le paso el estado de alerta como prop al componente de alerta-->
        <Alerta v-if="alerta.mensaje" :alerta="alerta">

        </Alerta>

        <!-- shadow md a    grega sobras, y rounded agrega border radius, px es padding en el eje x y py padding en ej ele y,  mb es margin button -->

        <!--subimt.prevent es igual que  e.preventDefault() en la funcion validar-->
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <div class="mb-5 ">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <!--inline event @input le coloca el valor colocado nombre y ya que nombre esta puesto arriba pues se actualiza en tiempo real-->

                <!--Una manera mucho mas sencilla es con v-model-->
                <input name="text" id="mascota" placeholder="Nombre de la masctoa"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" :value="nombre"
                    @input="$emit('update:nombre', $event.target.value)" />
            </div>

            <div class="mb-5 ">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">
                    Nombre Propietario
                </label>
                <input name="text" id="propietario" placeholder="Nombre del propietario"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md" :value="propietario"
                    @input="$emit('update:propietario', $event.target.value)" />
            </div>

            <div class="mb-5 ">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input id="email" type="email" placeholder="Email del propietario"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md" :value="email"
                    @input="$emit('update:email', $event.target.value)" />
            </div>

            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>
                <input id="alta" type="date" class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md"
                    :value="alta" @input="$emit('update:alta', $event.target.value)" />
            </div>

            <div class="mb-5 ">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>
                <textarea id="sintomas" placeholder="Describe los sintomas del paciente"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md h-40" :value="sintomas"
                    @input="$emit('update:sintomas', $event.target.value)" />
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                :value="[editando? 'Guardar Cambios': 'Registrar Paciente']" />
        </form>
    </div>
</template>
