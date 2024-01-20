<script setup>
    import { reactive } from 'vue'
    import Alerta from './Alerta.vue'


    const alerta =reactive({
        tipo:'',
        mensaje:'',

    });

    const emit = defineEmits([
        'update:nombre',
        'update:propietario',
        'update:email',
        'update:alta',
        'update:sintomas',
        'guardar-paciente'
    ]);

    const props = defineProps({
        nombre:{
            type: String,
            required: true
        },
        propietario:{
            type: String,
            required: true
        },
        email:{
            type: String,
            required: true
        },
        alta:{
            type: String,
            required: true
        },
        sintomas:{
            type: String,
            required: true
        },

    })

    const validar = ()=>{
        if(Object.values(props).includes('')){
            alerta.mensaje='Todos los campos son obligatorios';
            alerta.tipo='error';
            return;
        }
        emit('guardar-paciente');
        alerta.mensaje='Todo Ok';
        alerta.tipo='Success';
    }
</script>

<template>
    <div class="w-1/2 md:w/2">
        <h2 
            class="font-black text-3xl text-center mb-10"
        >
        Añade pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </h2>
        
        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />
            <form
                class="bg-white shadow-md rounded-lg py-10 px-5 md-10"
               @submit.prevent="validar"
            >
                <div
                    class="mb-5"
                >
                    <label
                        class="block text-gray-700 uppercase font-bold"
                        for="mascota">
                        Nombre Mascota
                    </label>
                    <input
                        type="text"
                        placeholder="Nombre de la mascota"
                        id="mascota"
                        name="mascota"
                        :value="nombre"
                        @input="$emit('update:nombre',$event.target.value)"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    />
                    
                </div>

                <div
                    class="mb-5"
                >
                    <label
                        class="block text-gray-700 uppercase font-bold"
                        for="propietario">
                        Nombre del propietario
                    </label>
                    <input
                        type="text"
                        placeholder="Nombre del propietario"
                        id="propietario"
                        name="propietario"
                        :value="propietario"
                        @input="$emit('update:propietario',$event.target.value)"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    />
                    
                </div>

                <div
                    class="mb-5"
                >
                    <label
                        class="block text-gray-700 uppercase font-bold"
                        for="email">
                        Email
                    </label>
                    <input
                        type="email"
                        placeholder="e-mail"
                        id="email"
                        name="email"
                        :value="email"
                        @input="$emit('update:email',$event.target.value)"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    />
                    
                </div>

                <div
                    class="mb-5"
                >
                    <label
                        class="block text-gray-700 uppercase font-bold"
                        for="alta">
                        Alta
                    </label>
                    <input
                        type="date"
                        id="alta"
                        name="alta"
                        :value="alta"
                        @input="$emit('update:alta',$event.target.value)"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    />
                    
                </div>

                <div
                    class="mb-5"
                >
                    <label
                        class="block text-gray-700 uppercase font-bold"
                        for="sintomas">
                        Sintomas
                    </label>
                    <textarea
                        id="sintomas"
                        name="sintomas"
                        :value="sintomas"
                        @input="$emit('update:sintomas',$event.target.value)"
                        placeholder="Describe los sintomas"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md resize-none h-40"
                    />
                    
                </div>

                <input type="submit"
                    value="Registrar Paciente"
                    class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors "
                
                />
            </form>
    </div>
</template>
