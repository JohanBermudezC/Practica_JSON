<script setup>
import { ref } from "vue";

const bancoPreguntas = [
    {
        pregunta: "¿Qué hace la fotosíntesis en las plantas?",
        respuestas: [
            { respuesta: "Transforma la luz solar en energía química", valor: true },
            { respuesta: "Produce dióxido de carbono", valor: false },
            { respuesta: "Consume agua y oxígeno", valor: false },
            { respuesta: "Genera calor", valor: false }
        ]
    },
    {
        pregunta: "¿Cuál es la capital de Francia?",
        respuestas: [
            { respuesta: "Madrid", valor: false },
            { respuesta: "Berlín", valor: false },
            { respuesta: "París", valor: true },
            { respuesta: "Londres", valor: false }
        ]
    },
    {
        pregunta: "¿Qué es el agua?",
        respuestas: [
            { respuesta: "Un elemento químico", valor: false },
            { respuesta: "Una mezcla heterogénea", valor: false },
            { respuesta: "Un compuesto químico", valor: true },
            { respuesta: "Un ion", valor: false }
        ]
    }
];

const indice = ref(0);
const ensenarPregunta = ref(bancoPreguntas[indice.value].pregunta);
const ensenarRespuestas = ref(bancoPreguntas[indice.value].respuestas);

const colors = [
    "bg-red-600",
    "bg-blue-600",
    "bg-yellow-600",
    "bg-green-600",
];

function pregunta() {
    if (indice.value < bancoPreguntas.length - 1) {
        indice.value++;
        actualizarPregunta();
    } else {
        indice.value++;
    }
}

function actualizarPregunta() {
    if (indice.value < bancoPreguntas.length) {
        ensenarPregunta.value = bancoPreguntas[indice.value].pregunta;
        ensenarRespuestas.value = bancoPreguntas[indice.value].respuestas;
        correcto.value = false;
    }
}

function validar(respuestaIndex) {
    const respuesta = ensenarRespuestas.value[respuestaIndex];
    if (respuesta.valor) {
        correcto.value = true;
        respuestasCorrectas.value++;
    } else {
        correcto.value = false;
        respuestasIncorrectas.value++;
    }
}

const correcto = ref(false);
const respuestasCorrectas = ref(0);
const respuestasIncorrectas = ref(0);
</script>

<template>
    <div class="w-full h-screen flex items-center">
        <div class="w-2/4 mx-auto bg-[#f2f2f2] p-4 rounded-md shadow-lg">
            <div v-if="indice < bancoPreguntas.length">
                <div class="w-full text-center text-xl font-semibold mb-4">{{ ensenarPregunta }}</div>
                <div class="mx-auto w-3/5 h-56 bg-[#32508e] flex justify-center items-center font-medium text-white text-[60px]"
                    :class="{ 'bg-green-700': correcto }">UFPSO</div>
                <div class="grid grid-cols-2 gap-1 mt-5">
                    <div v-for="(respuesta, i) in ensenarRespuestas" :key="i" class="cursor-pointer">
                        <div @click="validar(i)"
                            :class="[colors[i % colors.length], 'p-4', 'rounded-md', 'mb-2', 'cursor-pointer']">
                            {{ respuesta.respuesta }}
                        </div>
                    </div>
                </div>
                <button @click="pregunta" class="mt-4 bg-[#1a7b78] text-white py-2 px-4 rounded hover:bg-[#349e9b]">
                    Siguiente
                </button>
            </div>
            <div v-else>
                <div class="text-4xl text-center font-bold">Resultados</div>
                <div class="text-center mt-4">
                    <p class="text-lg">Respuestas correctas: {{ respuestasCorrectas }}</p>
                    <p class="text-lg">Respuestas incorrectas: {{ respuestasIncorrectas }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
