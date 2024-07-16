<script setup>
import { ref } from 'vue';
import { reactive } from 'vue';
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';
const pacientes = ref([]);


//agrupa los states de una manera sencilla
const paciente = reactive({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: '',
});


const guardarPaciente = () => {
  const nuevoPaciente = { ...paciente }; 
  Object.assign(paciente, {
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: '',
  });
  console.log('agregando paciente...');
  pacientes.value.push(nuevoPaciente);
  console.log(pacientes.value)
}
</script>

<template>
  <!-- esto centtra el header -->
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <!-- como movi paciente al componente padre app los v-models los tengo que pasar para el componente formulario -->
      <formulario
       v-model:nombre="paciente.nombre"
       v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center ">Administra tus Pacientes</h3>
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Informacion de
            <span class="text-indigo-600 font-bold">Pacientes</span>
        </p>
          <Paciente v-for="paciente in pacientes" :paciente="paciente"/>
        </div>
        <p v-else class="text-2xl text-center mt-20">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>