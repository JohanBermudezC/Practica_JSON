<script setup>
import { ref, computed } from 'vue';
const reportes = ref([
    {
        fecha: "10 junio del 2024",
        peso: "80",
        cintura: "78",
        cadera: "84"
    },
    {
        fecha: "10 junio del 2024",
        peso: "90",
        cintura: "78",
        cadera: "84"
    }
]);

const newFecha = ref("");
const newPeso = ref("");
const newCintura = ref("");
const newCadera = ref("");

function addReporte(){

    reportes.value.push({
        fecha: newFecha.value,
        peso: newPeso.value,
        cintura: newCintura.value,
        newCadera: newFecha.value
    });
    newFecha.value = "";
    newPeso.value = "";
    newCintura.value = "";
    newCadera.value = "";
}

const pesoPerdido = computed(function () {
    return calcularPeso();
});

const cinturaPerdida = computed(function () {
    return calcularCintura();
});

const caderaPerdida = computed(function () {
    return calcularCadera();
});

function calcularPeso(){
    if(reportes.value.length > 1){
        return parseInt(reportes.value[0].peso) - parseInt(reportes.value[reportes.value.length - 1].peso );
    }
   return 0 ;    
}

function calcularCintura(){
    if(reportes.value.length > 1){
        return parseInt(reportes.value[0].cintura) - parseInt(reportes.value[reportes.value.length - 1].cintura );
    }
   return 0 ;    
}
function calcularCadera(){
    if(reportes.value.length > 1){
        return parseInt(reportes.value[0].cadera) - parseInt(reportes.value[reportes.value.length - 1].cadera );
    }
   return 0 ;    
}
</script>

<template>

<div class="w-full h-screen flex items-center">
    <div class="w-2/4 bg-slate-500 p-3 mx-auto flex flex-col items-center">
        <div class="w-2/5 overflow-y-auto p-3 h-72">
            <div class=" mt-3 bg-slate-200" v-for="reporte in reportes" :key="i">
                <p class="bg-blue-600 text-slate-950 font-semibold text-center" >Fecha: {{reporte.fecha}}</p>
                <p>Peso: {{reporte.peso}} Kg</p>
                <p>Cintura: {{reporte.cintura}} cm</p>
                <p>Cadera: {{reporte.cadera}} cm</p>
            </div>
        </div>
            
        <div class="flex space-x-2 mt-5">
             <p>Peso perdido: {{ pesoPerdido }} Kg</p><span>|</span>
             <p>Reduccion de cintura: {{cinturaPerdida}} cm</p><span>|</span>
             <p>Reduccion de cadera: {{ caderaPerdida }} cm</p>
        </div>

        <div class="w-2/5 mt-5 bg-slate-200 flex flex-col items-center space-y-2 p-3">
            <input class="px-2 py-1" type="text"  placeholder="Fecha"v-model="newFecha" >
            <input class="px-2 py-1" type="text"  placeholder="Peso" v-model="newPeso">
            <input class="px-2 py-1" type="text"  placeholder="Talla cintura" v-model="newCintura">
            <input class="px-2 py-1" type="text"  placeholder="Talla cadera" v-model="newCadera">
            <div class="w-[183px]  grid justify-items-end">
                <button  @click="addReporte()" class=" bg-purple-700 px-2">Añadir</button>
            </div>
        </div>
    </div>
</div>
</template>









