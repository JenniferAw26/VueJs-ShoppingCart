<script setup>
  //Importando una funcion para crear referencias reactivas
  import { ref, computed } from 'vue'
 
  //Creando una referencia reactiva de tipo string
  const header = ref('App lista de compras');
  const shoppingIcon = ref("material-icons shopping-cart-icon")
 
  //Creando una referencia reactiva para almacenar el valor de la lista
  const items = ref([
  //{id: 0 , label: 'Leche', purchased: false, highPriority: true},
  //{id: 1 , label: 'Arroz', purchased: false, highPriority: false},
  //{id: 2 , label: 'Carne', purchased: true, highPriority: false},
  //{id: 3 , label: 'Pan', purchased: false, highPriority: true},
  //{id: 4 , label: 'Huevos', purchased: true, highPriority: true}
  ]);
 
  //Creacion de un metodo para poder modificar cada uno de nuestros items
  const togglePurchased = (item) =>
  {
    item.purchased = !item.purchased
  }
 
  const newItem = ref('');
  //Computed es uan propiedad computada, con valores dinamicos (calcula, hace algo, es una funcion) pueden leer referencia reactivas, pero no alterarlas
  const characterCount = computed(()=>{
    return newItem.value.length;
  });
  const newItemHighPriority = ref(false)
 
  //Creacion de Metodos, son funciones de javascript
  const saveItems = () => {
  //Agrega un nuevo elemento a la lista proveniente de la caja de texto
  items.value.push({
    id: items.value.length,
    label: newItem.value,
    highPriority:newItemHighPriority.value
  })
 
  //Borramos el contenido de la caja de texto
  newItem.value = "";
  newItemHighPriority.value = false;
};
 
const doEdit = (edit) => {
  editing.value = edit;
  newItem.value = "";
  newItemHighPriority.value = false;
}
const editing = ref(false);
</script>
 
<template>
  <!-- Header -->
  <div class="header">
    <h1>
      <i :class="shoppingIcon">local_mall</i>{{ header }}
    </h1>
    <button v-on:click="doEdit(false)" v-if="editing" class="btn">Cancelar</button>
    <button v-else v-on:click="doEdit(true)" class="btn btn-primary">Agregar Articulo</button>
  </div>
 
  <!-- Formulario -->
  <form
    v-if="editing"
    v-on:submit.prevent="saveItems"
    class="add-item form">
    <input
    v-model ="newItem" type="text"
    placeholder="Agregar Articulo">
 
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
    <p class="counter"> {{ characterCount }} / 200</p>
  </form>
 
  <!-- Entrega de Lista -->
  <ul>
    <li
    v-for="({ id, label, purchased, highPriority }, index) in items"
    @click="togglePurchased(items[index])"
    :class="{priority: highPriority, strikeout:purchased}"
    v-bind:key="id">
    🌟 {{ label }}
    </li>
  </ul>
 
  <!-- <ul>
    <li
    v-for="({ id, label, purchased, highPriority }, i) in items"
    :class="[purchased ? 'strikeout' : '', highPriority ? 'priority' : '']"
    v-bind:key="id">
    🌟 {{ label }}
    </li>
  </ul> -->
 
  <!-- Mensaje Condicional -->
  <p v-if="items.length === 0">🥀 No hay elementos en la lista 🥀</p>
</template>
 
<style scoped>
.shopping-cart-icon{
  font-size: 2rem;
}
</style>
tiene menú contextual


tienes menú contextual