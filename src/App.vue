<template>
  <div>
    <!-- Formulario de entrada para agregar nuevos nombres -->
    <form @submit.prevent="addName">
      <input v-model="newName" placeholder="Nombre" required>
      <input v-model="newLastName" placeholder="Apellido" required>
      <button type="submit">Agregar</button>
    </form>
    
    <!-- Lista de nombres existentes -->
    <ul>
      <li v-for="(name, index) in names" :key="index">
        {{ name.firstName }} {{ name.lastName }}
        <button @click="editName(index)">Editar</button>
        <button @click="deleteName(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newName = ref('');
const newLastName = ref('');
const names = ref([]);

function addName() {
  if (newName.value && newLastName.value) {
    names.value.push({ firstName: capitalize(newName.value), lastName: capitalize(newLastName.value) });
    newName.value = '';
    newLastName.value = '';
  }
}

function editName(index) {
  const editedName = prompt('Ingrese el nuevo nombre:');
  const editedLastName = prompt('Ingrese el nuevo apellido:');
  if (editedName && editedLastName) {
    names.value[index].firstName = capitalize(editedName);
    names.value[index].lastName = capitalize(editedLastName);
  }
}

function deleteName(index) {
  names.value.splice(index, 1);
}

function capitalize(string) {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
</script>