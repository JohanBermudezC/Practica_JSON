<script setup>
import { ref } from 'vue';

const selectedIndex = ref(-1);
const selectedIndexHijo = ref(-1);
const selectedIndexSubHijo = ref(-1);

const localC = ref([
  { name: 'Home', icono: '🏠' },
  { name: 'Galeria', icono: '🖼' },
  { name: 'OnDrive - personal', icono: '📁', hijo: [
      {
        name: 'Documentos', icono: '📁',
        hijo: [
          { name: 'Anvsoft', icono: '📁' },
          { name: 'Captura', icono: '📁' },
          { name: 'ClickCharts', icono: '📁' },
          { name: 'Custom Office Template', icono: '📁' },
          { name: 'OneNote Notebooks', icono: '📁' },
          { name: 'Sound Recordings', icono: '📁' },
          { name: 'Zoom', icono: '📁' },
          { name: 'Pictures', icono: '📁' },
          { name: 'TWC', icono: '📁' },
          { name: 'HOLA MUNDO', icono: '📁' },
        ]
      }
    ]
  }
]);

function showInfo(i) {
  if (i == selectedIndex.value) {
    selectedIndex.value = -1;
  } else {
    selectedIndex.value = i;
  }
}

function showInfoHijo(j) {
  if (j == selectedIndexHijo.value) {
    selectedIndexHijo.value = -1;
  } else {
    selectedIndexHijo.value = j;
  }
}

function showInfoSubHijo(k) {
  if (k == selectedIndexSubHijo.value) {
    selectedIndexSubHijo.value = -1;
  } else {
    selectedIndexSubHijo.value = k;
  }
}


function addFolder() {
  const newFolder = { name: 'Nueva Carpeta', icono: '📁', hijo: [] };

  if (selectedIndex.value !== -1 && selectedIndexHijo.value === -1) {
    if (!localC.value[selectedIndex.value].hijo) {
      localC.value[selectedIndex.value].hijo = [];
    }
    localC.value[selectedIndex.value].hijo.push(newFolder);
  } else if (selectedIndexHijo.value !== -1 && selectedIndexSubHijo.value === -1) {
    if (!localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo) {
      localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo = [];
    }
    localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo.push(newFolder);
  } else if (selectedIndexSubHijo.value !== -1) {
    if (!localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo[selectedIndexSubHijo.value].hijo) {
      localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo[selectedIndexSubHijo.value].hijo = [];
    }
    localC.value[selectedIndex.value].hijo[selectedIndexHijo.value].hijo[selectedIndexSubHijo.value].hijo.push(newFolder);
  } else {
    alert('Seleccione una carpeta para añadir una subcarpeta.');
  }
}

function addFile() {
  if (selectedIndex.value !== -1) {
    const newFile = { name: 'Nuevo Archivo', icono: '📄' };
    if (localC.value[selectedIndex.value].hijo) {
      localC.value[selectedIndex.value].hijo.push(newFile);
    } else {
      localC.value[selectedIndex.value].hijo = [newFile];
    }
  } else {
    alert('Seleccione una carpeta para añadir un archivo.');
  }
}
</script>

<template>
  <div class="flex items-center w-full h-screen bg-slate-200">
    <div class="mx-auto w-2/4 h-96 flex space-x-8">
      <div class="bg-slate-100 w-[300px] overflow-y-auto">
        <div v-for="(carpeta, i) in localC" :key="i" class="px-2 cursor-pointer">
          <span @click="showInfo(i)">
            <span>{{ selectedIndex == i ? 'v' : '>' }}</span> {{ carpeta.icono }} {{ carpeta.name }}</span>

          <div v-show="selectedIndex == i" class="px-2">
            <ul v-for="(hijo, j) in carpeta.hijo" :key="j" class="ml-4">
              <span @click="showInfoHijo(j)">
                <span>{{ selectedIndexHijo == j ? 'v' : '>' }}</span> {{ hijo.icono }} {{ hijo.name }}
              </span>

              <div v-show="selectedIndexHijo == j">
                <li v-for="(subHijo, k) in hijo.hijo" :key="k" class="px-2">
                  <span @click="showInfoSubHijo(k)">
                    {{ selectedIndexSubHijo == k ? 'v' : '>' }} {{ subHijo.icono }} {{ subHijo.name }}
                  </span>
                </li>
              </div>
            </ul>
          </div>
        </div>
      </div>
      <div class="w-56 bg-gray-300 mt-12 h-56 flex items-center flex-col">
        <h1>Añadir archivo/carpeta</h1>
        <button class="w-4/5 my-2 bg-blue-500 text-white p-2 rounded" @click="addFolder">Añadir Carpeta</button>
        <button class="w-4/5 my-2 bg-green-500 text-white p-2 rounded" @click="addFile">Añadir Archivo</button>
      </div>
    </div>
  </div>
</template>
