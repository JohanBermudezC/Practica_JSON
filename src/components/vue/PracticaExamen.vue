<script setup>
import { ref } from 'vue';

const options = ref([
  { label: 'Entre los 14 y 18 años', count: 0, bgColor: 'bg-blue-600' },
  { label: 'Entre los 19 y 25 años', count: 0, bgColor: 'bg-teal-500' },
  { label: 'Entre los 26 y 45 años', count: 0, bgColor: 'bg-blue-400' },
  { label: 'Mayor de 45 años', count: 0, bgColor: 'bg-yellow-500' },
]);

const selectedOption = ref(null);
const showResults = ref(false);
const totalCount = ref(0);

const selectOption = (index) => {
  selectedOption.value = index;
};

const register = () => {
  if (selectedOption.value !== null) {
    options.value[selectedOption.value].count++;
    totalCount.value++;
    showResults.value = true;
    selectedOption.value = null;
  }
};

const reset = () => {
  options.value.forEach(option => option.count = 0);
  totalCount.value = 0;
  showResults.value = false;
};

const getPercentage = (count) => {
  return totalCount.value === 0 ? 0 : ((count / totalCount.value) * 100).toFixed(0);
};
</script>


<template>
    <div class="p-6">
      <h2 class="text-xl font-bold mb-4">¿En qué rango de edad se encuentra?</h2>
      <div v-for="(option, index) in options" :key="index" class="mb-2">
        <button
          @click="selectOption(index)"
          :class="[
            'w-full py-2 text-white font-bold rounded',
            selectedOption === index ? 'bg-blue-800' : option.bgColor
          ]"
        >
          {{ option.label }}
        </button>
      </div>
      <button
        @click="register"
        class="w-full py-2 mt-4 bg-red-500 text-white font-bold rounded"
        :disabled="selectedOption === null"
      >
        Registrar
      </button>
  
      <div v-if="showResults" class="mt-6">
        <h3 class="text-lg font-bold mb-2">Resultados Parciales</h3>
        <div v-for="(option, index) in options" :key="'result-' + index" class="mb-2">
          <div class="flex justify-between">
            <span>{{ option.label }}</span>
            <span>{{ getPercentage(option.count) }}%</span>
          </div>
          <div class="bg-gray-200 rounded h-4">
            <div
              :class="[option.bgColor, 'h-4 rounded']"
              :style="{ width: getPercentage(option.count) + '%' }"
            ></div>
          </div>
        </div>
        <button
          @click="reset"
          class="w-full py-2 mt-4 bg-red-500 text-white font-bold rounded"
        >
          Registrar nuevamente
        </button>
      </div>
    </div>
  </template>
  


    
    
  
  
  