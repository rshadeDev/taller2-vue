<template>
  <div class="formulario">
    <form @submit.prevent="agregarNombre">
      <input v-model="nuevoNombre" placeholder="Ingresa tu nombre" required>
      <input v-model="nuevoApellido" placeholder="Ingresa tu apellido" required>
      <button type="submit">Agregar nombre</button>
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
    names.value.push({ nombre: capitalize(nuevoNombre.value), apellido: capitalize(nuevoApellido.value) });
    nuevoNombre.value = '';
    nuevoApellido.value = '';
  }
}

function editarNombre(index) {
  const editedName = prompt('Ingrese el nuevo nombre:');
  const editedLastName = prompt('Ingrese el nuevo apellido:');
  if (editedName && editedLastName) {
    names.value[index].nombre = capitalize(editedName);
    names.value[index].apellido = capitalize(editedLastName);
  }
}

function borrarNombre(index) {
  names.value.splice(index, 1);
}

function capitalize(string) {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
</script>

<style scoped>
form {
  margin-bottom: 20px;
}
input {
  margin-right: 10px;
  padding: 5px;
  border-radius: 10px;
  border: none;
}
button {
  padding: 5px 10px;
  background-color: black;
  color: white;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
button:hover {
  background-color: darkslateblue;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin-bottom: 10px;
}
li button {
  margin-left: 10px;
}
.formulario {
  display: flex;
  justify-content: center;
  flex-direction: column;
  height: 30vh;
  background-color: lightblue;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
  padding: 20px;
  border-radius: 10px;
  position: absolute;
  top: calc(50% - 10px);
  left: calc(50% - 10px);
  transform: translate(-50%, -50%);
}
</style>