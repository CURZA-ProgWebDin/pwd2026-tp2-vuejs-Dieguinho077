<script setup>
import { ref, computed } from 'vue'
import ProductForm from './components/ProductForm.vue'
import ProductList from './components/ProductList.vue'

const productos = ref([])

const crearProducto = (objetoForm) => {

  const nuevoProducto = {
    id: Date.now(), 
    nombre: objetoForm.nombre,
    precio: objetoForm.precio,
    stock: objetoForm.stock,
    categoria: objetoForm.categoria
  }
  
  productos.value.push(nuevoProducto)
}

const eliminarProducto = (indice) => { 
  productos.value.splice(indice, 1) 
}

const cantidadTotal = computed(() => {
  return productos.value.length
})

const valorInventario = computed(() => {
  let total = 0
  for (let p of productos.value) {
    total = total + (p.precio * p.stock)
  }
  return total
})
</script>

<template>
  <div class="app">
    <header>
      <h1>Gestión de Productos</h1>
    </header>

    <ProductForm @add-product="crearProducto" />

    <section class="resumen">
      <p>Cantidad de productos: <strong>{{ cantidadTotal}}</strong></p>
      <p>Valor total inventario: <strong>${{ valorInventario }}</strong></p>
    </section>

    <ProductList 
      :productos="productos" 
      @delete-product="eliminarProducto" 
    />
  </div>
</template>

<style>
.app { font-family: Arial, sans-serif; max-width: 900px; margin: 0 auto; padding: 20px; }
h1 { color: #5e2a8e; border-bottom: 2px solid #5e2a8e; }
.resumen { background: #f4f0fa; padding: 15px; border-radius: 8px; margin: 20px 0; border-left: 5px solid #5e2a8e; }
</style>