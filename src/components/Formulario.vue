<script setup>
import { reactive } from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    tipo: '',
    mensaje:''
})

//agrupa los states de una manera sencilla
const paciente = reactive({
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: '',
})
 
const validar = () => {
    if (Object.values(paciente).includes('')) {
        alerta.mensaje = "Todos los campos son obligarorios"
        alerta.tipo = "error"
        return
    }
}

</script>

<template>
    <div class="md:1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>

        <Alerta v-if="alerta.mensaje" :alerta="alerta">
            
        </Alerta>

        <!-- shadow md a    grega sobras, y rounded agrega border radius, px es padding en el eje x y py padding en ej ele y,  mb es margin button -->

        <!--subimt.prevent es igual que  e.preventDefault() en la funcion validar-->
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
                @submit.prevent="validar"
        >
            <div class="mb-5 ">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <!--inline event @input le coloca el valor colocado nombre y ya que nombre esta puesto arriba pues se actualiza en tiempo real-->

                <!--Una manera mucho mas sencilla es con v-model-->
                <input name="text" id="mascota" placeholder="Nombre de la masctoa"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                    v-model="paciente.nombre" />

            </div>

            <div class="mb-5 ">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">
                    Nombre Propietario
                </label>
                <input name="text" id="propietario" placeholder="Nombre del propietario"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md"
                    v-model="paciente.propietario">
            </div>

            <div class="mb-5 ">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input id="email" type="email" placeholder="Email del propietario"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md"
                    v-model="paciente.email">
            </div>

            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>
                <input id="alta" type="date" class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md"
                v-model="paciente.alta">
            </div>

            <div class="mb-5 ">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>
                <textarea id="sintomas" placeholder="Describe los sintomas del paciente"
                    class="border-2 w-full p-2 mt=2 placeholder-gray-400 rounded-md h-40"
                    v-model="paciente.sintomas" />
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar Pacientes">
        </form>
    </div>
</template>
