
<script setup>
import { ref, computed } from 'vue';

const candidates = ref([
  { id: 1, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 5 },
  { id: 2, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 4 },
  { id: 3, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 3 },
  { id: 4, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 5 },
  { id: 5, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 4 },
  { id: 6, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 5 },
  { id: 7, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 3 },
  { id: 8, name: 'Michael Deo', position: 'UI/UX Designer', address: '795 Folsom Ave, Suite 600 San Francisco, CA 94107', image: 'https://via.placeholder.com/50', stars: 4 }
]);

const currentPage = ref(1);
const itemsPerPage = 4;

const paginatedCandidates = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return candidates.value.slice(start, start + itemsPerPage);
});

const hasPrevious = computed(() => currentPage.value > 1);
const hasNext = computed(() => currentPage.value * itemsPerPage < candidates.value.length);

const previousPage = () => {
  if (hasPrevious.value) currentPage.value--;
};

const nextPage = () => {
  if (hasNext.value) currentPage.value++;
};

const newCandidate = ref({
  id: candidates.value.length + 1,
  name: '',
  position: '',
  address: '',
  image: '',
  stars: 1
});

const addCandidate = () => {
  if (newCandidate.value.name && newCandidate.value.position && newCandidate.value.address && newCandidate.value.stars) {
    candidates.value.push({ ...newCandidate.value, id: candidates.value.length + 1 });
    newCandidate.value = { id: candidates.value.length + 1, name: '', position: '', address: '', image: '', stars: 1 };
  }
};
</script>

<template>
  <div class="max-w-2xl mx-auto bg-white rounded-xl shadow-md overflow-hidden">
    <form @submit.prevent="addCandidate" class="p-4">
      <div class="mb-4">
        <label for="name" class="block text-gray-700">Nombre:</label>
        <input v-model="newCandidate.name" type="text" id="name" class="mt-1 p-2 border rounded w-full" required>
      </div>
      <div class="mb-4">
        <label for="position" class="block text-gray-700">Posición:</label>
        <input v-model="newCandidate.position" type="text" id="position" class="mt-1 p-2 border rounded w-full" required>
      </div>
      <div class="mb-4">
        <label for="address" class="block text-gray-700">Dirección:</label>
        <input v-model="newCandidate.address" type="text" id="address" class="mt-1 p-2 border rounded w-full" required>
      </div>
      <div class="mb-4">
        <label for="image" class="block text-gray-700">URL de Imagen:</label>
        <input v-model="newCandidate.image" type="url" id="image" class="mt-1 p-2 border rounded w-full">
      </div>
      <div class="mb-4">
        <label for="stars" class="block text-gray-700">Estrellas:</label>
        <input v-model="newCandidate.stars" type="number" id="stars" class="mt-1 p-2 border rounded w-full" min="1" max="5" required>
      </div>
      <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded">Agregar Candidato</button>
    </form>
    
    <div v-for="candidate in paginatedCandidates" :key="candidate.id" class="flex items-center space-x-4 p-4 border-t">
      <img :src="candidate.image" alt="" class="w-12 h-12 rounded-full" />
      <div class="flex-1">
        <div class="text-xl font-medium text-black">{{ candidate.name }}</div>
        <p class="text-gray-500">{{ candidate.position }}</p>
        <p class="text-gray-500">{{ candidate.address }}</p>
        <div class="flex items-center">
          <span class="text-yellow-500" v-for="n in candidate.stars" :key="n">★</span>
        </div>
      </div>
      <div class="flex space-x-2">
        <button class="px-3 py-1 bg-blue-500 text-white rounded">Follow</button>
        <button class="px-3 py-1 bg-blue-500 text-white rounded">Message</button>
      </div>
    </div>
    
    <div class="flex justify-between p-4 border-t">
      <button @click="previousPage" :disabled="!hasPrevious" class="px-3 py-1 bg-gray-300 text-black rounded" :class="{ 'opacity-50': !hasPrevious }">Anterior</button>
      <button @click="nextPage" :disabled="!hasNext" class="px-3 py-1 bg-gray-300 text-black rounded" :class="{ 'opacity-50': !hasNext }">Siguiente</button>
    </div>
  </div>
</template>

