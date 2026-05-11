<script setup>
import { ref, computed } from 'vue'
import ProductItem from './ProductItem.vue'

const props = defineProps(['listaProductos'])

const emit = defineEmits(['quitar-producto'])

const filtroCategoria = ref('')

const productosFiltrados = computed(() => {
  if (filtroCategoria.value === '') {
    return props.listaProductos
  }
  return props.listaProductos.filter(p => p.categoria === filtroCategoria.value)
})

const retransmitirEliminar = (id) => {
  emit('quitar-producto', id)
}
</script>

<template>
  <div class="tabla-contenedor">
    <h3>Listado de Stock</h3>

    <div class="filtro">
      <label>Filtrar por Categoría: </label>
      <select v-model="filtroCategoria">
        <option value="">Mostrar todos</option>
        <option value="Electrónica">Electrónica</option>
        <option value="Hogar">Hogar</option>
        <option value="Ropa">Ropa</option>
      </select>
    </div>

    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Stock</th>
          <th>Categoría</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <ProductItem 
          v-for="p in productosFiltrados" 
          :key="p.id" 
          :unProducto="p"
          @borrar-id="retransmitirEliminar"
        />
      </tbody>
    </table>
    
    <p v-if="productosFiltrados.length === 0" style="text-align: center;">
      No hay productos cargados en esta categoría.
    </p>
  </div>
</template>

<style scoped>
.tabla-contenedor { margin-top: 30px; }
table { width: 100%; border-collapse: collapse; }
th { background-color: #5e2a8e; color: white; padding: 10px; }
.filtro { margin-bottom: 15px; background: #eee; padding: 10px; border-radius: 5px; }
</style>