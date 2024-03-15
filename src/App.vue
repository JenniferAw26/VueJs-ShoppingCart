<script setup>
//Importando una funcion para crear referencias reactivas
import { ref } from 'vue'
//Creando una referencia reactiva de tipo string
const header = ref('App lista de compras');
const shoppingIcon = ref("material-icons shopping-cart-icon")
//Creando una referencia reactiva para almacenar el valor de la lista
const items = ref([
// {id: 0 , label: 'Leche'},
// {id: 1 , label: 'Arroz'},
// {id: 2 , label: 'Carne'},
// {id: 3 , label: 'Pan'},
// {id: 4 , label: 'Huevos'}
]);
 
const newItem = ref('');
const newItemHighPriority = ref(false)
const showForm = ref(false); // Se crea variable reactiva para controlar la visibilidad de los botones en el formulario
 
//Metodos, son funciones de javascript
const saveItems = () => {
  //Agrega un nuevo elemento a la lista proveniente de la caja de texto
  items.value.push({ id: items.value.length, label: newItem.value})
  //Borramos el contenido de la caja de texto
  newItem.value = "";
};
 //Entrega Condicional
//const noItemsMessage =ref (true); cuando requiero alterar un valor de una variable, este debe alterar el metodo
</script>
 
<template>
  <!-- Header -->
  <div class="header">
    <h1> <i :class="shoppingIcon">local_mall</i>{{ header }}</h1>
    <button v-if="showForm" class="btn" @click="showForm = false">Cancelar ❌</button>
    <button v-else  class="btn" @click="showForm = true">Agregar Articulo ✅</button>  
    <!-- ! significa negativo -->
  </div>
  <!-- Formulario -->
  <form v-if="showForm"
    v-on:submit.prevent="saveItems"
    class="add-item form">
    <input v-model="newItem" type="text" placeholder="Agregar Articulo">
 
    <!-- Checkbox -->
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      Alta Prioridad
    </label>
 
    <!-- Boton -->
    <button
      class="btn btn-primary">
      Agregar Articulo
    </button>
  </form>
 <!-- Entrega de lista -->
  <ul>
    <li v-for="({ id, label }, i) in items" v-bind:key="id">🌟 {{ i }} {{ label }}</li>
  </ul>
  <!-- Mensaje condicional -->
 <p v-if="items.length === 0"> 🥀No hay elementos en la lista🥀</p> 
</template>
 
<style scoped>
.shopping-cart-icon{
  font-size: 2rem;
}
</style>
