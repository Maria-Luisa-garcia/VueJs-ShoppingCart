<script setup>
import { ref } from 'vue'
const header = ref('App Lista de compras')
const items = ref([
  //{id: 1, label: '10 bolillos'},
  //{id: 2, label: '1 lata de frijoles'},
  //{id: 3, label: '2 lata de atún'}
])
//Agregando todo para giardar nuevo articulo
const saveItem = () => {
  // codigo para verificar si newItem no está vacío antes de agregarlo a la lista
  if (newItem.value.trim() !== '') {
    items.value.push({ id: items.value.length + 1, label: newItem.value })
    // Borrar o limpiar la caja de texto de newItem
    newItem.value = ''
  }
}
const newItem = ref('')
const newItemHighPriority = ref(false)
const habilitarFormulario = ref(false)
//Creo la nueva variable
const DoEdit = (edit) => {
  //Le coloco la accion de que sea igual a un valor
  habilitarFormulario.value = edit
  //Le coloco la accion de borrar la caja de texto
  newItem.value = ''
}
</script>
<template>
  <div class="header">
    <h1><i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
    <button v-if="!habilitarFormulario" @click="DoEdit(true)" class="btn btn-primary">
      Agregar articulo
    </button>
    <button v-else @click="DoEdit(false)" class="btn">Cancelar</button>
  </div>
  <!--  Esto se usa para crear un ipervinculo con una imagen dependiendo de lo que escribas en la 
    caja de texto
  <a :href="newItem">
  <i class="material-icons shopping-cart-icon">school</i>
</a>-->
  <form v-if="habilitarFormulario" v-on:submit.prevent="saveItem" class="add-item form">
    <!-- Input de Nuevo Articulo -->
    <input v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo" />
    <!-- Check Boxes -->
    <label>
      <input v-model="newItemHighPriority" type="checkbox" />
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? '🔥' : '🧊' }}
    <!-- Boton de UI -->
    <button class="btn btn-primary">Salvar Articulo</button>
  </form>
  <ul>
    <li v-for="{ id, label } in items" v-bind:key="id">♥ {{ label }}</li>
  </ul>
  <p v-if="items.length == 0">🌹Lista de compras vacia🥀</p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
