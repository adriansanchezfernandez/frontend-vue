<script setup lang="ts">
import { ref } from 'vue'
import SavingGoals from './components/SavingGoals.vue'

const objetivos = ref([
  {
    id: 1,
    nombre: 'Viaje a Japón',
    ahorrado: 1200,
    cantidadObjetivo: 3000,
  },
  {
    id: 2,
    nombre: 'Ordenador nuevo',
    ahorrado: 450,
    cantidadObjetivo: 1500,
  },
  {
    id: 3,
    nombre: 'Vacaciones',
    ahorrado: 800,
    cantidadObjetivo: 2000,
  },
])

function agregarAhorro(id: number) {
  const objetivo = objetivos.value.find((o) => o.id === id)

  if (objetivo) {
    objetivo.ahorrado = Math.min(objetivo.ahorrado + 100, objetivo.cantidadObjetivo)
  }
}
</script>

<template>
  <main>
    <h1>Mis objetivos de ahorro</h1>

    <div class="objetivos">
      <SavingGoals
        v-for="objetivo in objetivos"
        :key="objetivo.id"
        :nombre="objetivo.nombre"
        :ahorrado="objetivo.ahorrado"
        :cantidad-objetivo="objetivo.cantidadObjetivo"
        @agregar-ahorro="agregarAhorro(objetivo.id)"
      />
    </div>
  </main>
</template>

<style scoped>
main {
  padding: 24px;
}

button {
  padding: 10px 16px;
  cursor: pointer;
}
</style>
