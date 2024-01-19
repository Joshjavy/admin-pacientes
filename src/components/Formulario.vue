<script setup>

</script>

<template>
    <div class="w-1/2 md:w/2">
        <h2 
            class="font-black text-3xl text-center"
        >
            Seguimientpo Paciente
        </h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
            <form
                class="bg-white shadow-md rounded-lg py-10 px-5 md-10"
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
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    />
                    
                </div>
            </form>

        </p>
    </div>
</template>
