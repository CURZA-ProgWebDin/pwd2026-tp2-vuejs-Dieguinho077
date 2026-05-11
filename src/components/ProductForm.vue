<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-product'])

const nombre = ref('')
const precio = ref(0)
const stock = ref(0)
const categoria = ref('')

const enviarFormulario = () => {
  if (nombre.value === '' || categoria.value === '') {
    alert("Falta completar")
    return
  }

  const datosParaEnviar = {
    nombre: nombre.value,
    precio: precio.value,
    stock: stock.value,
    categoria: categoria.value
  }

  emit('add-product', datosParaEnviar)

  nombre.value = ''
  precio.value = 0
  stock.value = 0
  categoria.value = ''
}
</script>

<template>
  <section class="formulario">
    <h3>Nuevo Producto</h3>
    <form @submit.prevent="enviarFormulario">
      <input v-model="nombre" type="text" placeholder="Nombre del producto">
      <input v-model.number="precio" type="number" placeholder="Precio">
      <input v-model.number="stock" type="number" placeholder="Stock">
      
      <select v-model="categoria">
        <option value="" disabled>Seleccione Categoría</option>
        <option value="Electrónica">Electrónica</option>
        <option value="Hogar">Hogar</option>
        <option value="Ropa">Ropa</option>
      </select>

      <button type="submit">Guardar Producto</button>
    </form>
  </section>
</template>

<style scoped>
.formulario {
  padding: 20px;
  border: 2px dashed #5e2a8e;
  border-radius: 10px;
}
input, select, button {
  display: block;
  margin: 10px 0;
  padding: 8px;
  width: 100%;
}
button {
  background-color: #5e2a8e;
  color: white;
  cursor: pointer;
  font-weight: bold;
}
</style>