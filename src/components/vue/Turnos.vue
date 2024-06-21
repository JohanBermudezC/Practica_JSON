<script setup>
import { ref } from 'vue';

const modulo1 = ref(["XASS55"]);
const modulo2 = ref(["XASS55"]);
const modulo3 = ref(["XASS55"]);

const opcionModulo = ref("modulo1");
const newCodigo = ref('');


function addTurno(){
    if(opcionModulo.value === "modulo1"){
        modulo1.value.push(newCodigo.value);
    }else if(opcionModulo.value === "modulo2"){
        modulo2.value.push(newCodigo.value);
    }else if(opcionModulo.value === "modulo3"){
        modulo3.value.push(newCodigo.value);
    }
    newCodigo.value = "";
    opcionModulo.value = "";
}

const contador = ref(modulo1.value.length + modulo2.value.length + modulo3.value.length);

</script>

<template>

<div class="w-full h-screen flex items-center bg-slate-400">
    
<div class="w-[60%] bg-white mx-auto px-5 py-8 ">
    <div class="w-full flex justify-center font-semibold text-[#30px] mb-5">
        <h1>SISTEMA DE TURNOS </h1>
    </div>

    <div class="w-full flex gap-3">
        <div class="w-[33%] bg-[#F5F5F5]">
            <h2 class=" text-white font-semibold bg-[#068fd3] px-3 py-2 text-center" >MÓDULO 1</h2>
            <div class="p-2 py-3">
                <p
                v-for="(codigo,i) in modulo1" :key="i++"
                 class="bg-white mt-3 px-2" >{{i}}-{{codigo}}</p>
            </div>
        
        </div>
        <div class="w-[33%] bg-[#F5F5F5]">
            <h2 class=" text-white font-semibold bg-[#d78846] px-3 py-2 text-center" >MÓDULO 2</h2>
            <div class="p-2 py-3">
                <p
                v-for="(codigo,i) in modulo2" :key="i++"
                 class="bg-white mt-3 px-2" >{{i}}-{{codigo}}</p>
            </div>
        
        </div>
        <div class="w-[33%] bg-[#F5F5F5]">
            <h2 class=" text-white font-semibold bg-[#308446] px-3 py-2 text-center" >MÓDULO 3</h2>
            <div class="p-2 py-3">
                <p
                v-for="(codigo,i) in modulo3" :key="i++"
                 class="bg-white mt-3 px-2" >{{i}}-{{codigo}}</p>
            </div>
        </div>
    </div>

    <div class="w-full flex justify-between bg-[#F5F5F5] mt-3 h-16 items-center px-3 font-semibold">
        <p class=" text-[20px]" >{{contador}} Turnos</p>
        <div class="space-x-3">
            <input type="text" placeholder="Código" class="border border-gray-400 rounded-[4px] py-1 pl-3 w-36" v-model="newCodigo">
            <select class="border border-gray-400 rounded-sm px-3 py-1 w-36" v-model="opcionModulo">
                <option value="modulo1" >Módulo 1</option>
                <option value="modulo2" >Módulo 2</option>
                <option value="modulo3" >Módulo 3</option>
            </select>
            <button class="bg-[#b786be] text-white px-3 py-1 rounded-[4px]"@click="addTurno" >Agregar Turno</button>
        </div>
    </div>
</div>
</div>

</template>