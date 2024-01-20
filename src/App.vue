<script setup>
  import { ref,reactive, onMounted, watch } from 'vue';
  import {uid }   from 'uid';
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Paciente from './components/Paciente.vue';

  const pacientes = ref([])

  const paciente = reactive({
    id:null,
    nombre:'',
    propietario:'',
    email:'',
    alta:'',
    sintomas:'',

  });

  watch(
    pacientes,()=>{
      guardarLocalStorage();
    },{
      deep:true
    }
  );

  onMounted(()=>{
    const pacientesStorage= localStorage.getItem('admsPacientes');
    if(pacientesStorage){
      pacientes.value = JSON.parse(pacientesStorage);
    }
  });

  const guardarLocalStorage=()=>{
    localStorage.setItem('admsPacientes',JSON.stringify(pacientes.value))
  }


  const guardarPaciente=()=>{
    if(paciente.id){
      const { id }= paciente;
      const i = pacientes.value.findIndex( paciente => paciente.id === id )

      pacientes.value[i] = {...paciente}
    }else{
      pacientes.value.push({...paciente,id:uid()});
    }
    

    //reiniciar el objeto
    // paciente.nombre='';
    // paciente.propietario='';
    // paciente.email='';
    // paciente.alta='';
    // paciente.sintomas='';

    //otra forma

    Object.assign(paciente,{
      nombre:'',
      propietario:'',
      email:'',
      alta:'',
      sintomas:'',
      id:null

    })
  }

  const actualizarPaciente= id =>{
    const pacienteEditar= pacientes.value.filter(paciente => paciente.id === id)[0]
    Object.assign(paciente,pacienteEditar)
  }

  const eliminarPaciente= id =>{
    pacientes.value = pacientes.value.filter(paciente=> paciente.id !== id)
  }
</script>

<template>
  <div class="container mx-auto met-20">
    <Header />
    
    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        :id="paciente.id"
        @guardar-paciente="guardarPaciente"
      />

      <div 
        class="w-1/2 md:w-1/2 md:h-screen overflow-y-scroll"
      >
      <h3
        class="font-black text-3xl text-center"
      >
        Pacientes Registrados
      </h3>
      <div
        v-if="pacientes.length >0 "
      >
        <Paciente
          v-for="paciente in pacientes"
          :paciente="paciente"
          @actualizar-paciente="actualizarPaciente"
          @eliminar-paciente="eliminarPaciente"
        />
      </div>
      <p 
        v-else class="mt-10 text-2xl text-center"
      >
        Aún no registra ningún paciente
      </p>


      </div>

    </div>
  </div>
</template>

