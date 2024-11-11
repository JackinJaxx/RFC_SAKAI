<script setup>
import { ref } from 'vue';

const nombre = ref('');
const apellidoPaterno = ref('');
const apellidoMaterno = ref('');
const fechaNacimiento = ref('');
const rfc = ref('');
const loading = ref(false);

function generarRFC() {
    loading.value = true;
    setTimeout(() => {
        if (nombre.value && apellidoPaterno.value && apellidoMaterno.value && fechaNacimiento.value) {
            // Obtener las primeras letras y fecha
            const primeraLetraPaterno = apellidoPaterno.value.charAt(0).toUpperCase();
            const primerasLetrasMaterno = apellidoMaterno.value.charAt(0).toUpperCase();
            const primerasLetrasNombre = nombre.value.charAt(0).toUpperCase();
            const fecha = new Date(fechaNacimiento.value);
            const anio = fecha.getFullYear().toString().slice(-2);
            const mes = (fecha.getMonth() + 1).toString().padStart(2, '0');
            const dia = fecha.getDate().toString().padStart(2, '0');

            // Generar el RFC
            rfc.value = `${primeraLetraPaterno}${primerasLetrasMaterno}${primerasLetrasNombre}${anio}${mes}${dia}`;
        } else {
            rfc.value = 'Por favor, completa todos los campos.';
        }
        loading.value = false;
    }, 1000);
}
</script>

<template>
    <Fluid>
        <div class="flex flex-col md:flex-row gap-8">
            <div class="md:w-1/2">
                <div class="card flex flex-col gap-4">
                    <div class="font-semibold text-xl">Generar RFC</div>

                    <div class="flex flex-col gap-2">
                        <label for="nombre">Nombre</label>
                        <InputText id="nombre" v-model="nombre" type="text" />
                    </div>

                    <div class="flex flex-col gap-2">
                        <label for="apellidoPaterno">Apellido Paterno</label>
                        <InputText id="apellidoPaterno" v-model="apellidoPaterno" type="text" />
                    </div>

                    <div class="flex flex-col gap-2">
                        <label for="apellidoMaterno">Apellido Materno</label>
                        <InputText id="apellidoMaterno" v-model="apellidoMaterno" type="text" />
                    </div>

                    <div class="flex flex-col gap-2">
                        <label for="fechaNacimiento">Fecha de Nacimiento</label>
                        <InputText id="fechaNacimiento" v-model="fechaNacimiento" type="date" />
                    </div>

                    <div class="flex flex-wrap gap-2 mt-4">
                        <Button label="Generar RFC" icon="pi pi-check" :loading="loading" @click="generarRFC" />
                    </div>

                    <div class="font-semibold text-xl">RFC Generado</div>
                    <div class="border p-4 rounded">
                        {{ rfc }}
                    </div>
                </div>
            </div>
        </div>
    </Fluid>
</template>
