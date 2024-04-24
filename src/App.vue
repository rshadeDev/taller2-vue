<template>
  <div>
    <form @submit.prevent="agregarNombre">
      <input v-model="nuevoNombre" placeholder="Ingresa un Nombre" required>
      <input v-model="nuevoApellido" placeholder="Ingrea un Apellido" required>
      <button type="submit">Agregar</button>
    </form>

    <ul>
      <li v-for="(name, index) in names" :key="index">
        {{ name.nombre }} {{ name.apellido }}
        <button @click="editarNombre(index)">Editar</button>
        <button @click="borrarNombre(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script setup>

import { ref } from 'vue';

const nuevoNombre = ref('');
const nuevoApellido = ref('');
const names = ref([]);

function agregarNombre() {
  if (nuevoNombre.value && nuevoApellido.value) {
    names.value.push({ nombre: capitalLetter(nuevoNombre.value), apellido: capitalLetter(nuevoApellido.value) });
    nuevoNombre.value = '';
    nuevoApellido.value = '';
  }
}

function editarNombre(index) {
  const editarNombre = prompt("Ingrese el nuevo nombre:");
  const editarApellido = prompt("Ingrese el nuevo apellido:");
  
  if (editarNombre && editarApellido) {
    names.value[index].nombre = capitalLetter(editarNombre);
    names.value[index].apellido = capitalLetter(editarApellido);
  }
}

function borrarNombre(index) {
  if (index >= 0 && index < names.value.length) {
    names.value.splice(index, 1);
  }
}

function capitalLetter(string) {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
</script>