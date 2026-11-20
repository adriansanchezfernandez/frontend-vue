<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  nombre: string
  ahorrado: number
  cantidadObjetivo: number
}>()

const emit = defineEmits<{
  agregarAhorro: []
}>()

const porcentaje = computed(() => {
  return props.cantidadObjetivo > 0 ? (props.ahorrado / props.cantidadObjetivo) * 100 : 0
})
</script>

<template>
  <article class="savings-goal">
    <h2>{{ nombre }}</h2>

    <p>{{ ahorrado }} € de {{ cantidadObjetivo }} €</p>

    <p>Progreso: {{ porcentaje.toFixed(1) }} %</p>

    <progress :value="Math.min(porcentaje, 100)" max="100"></progress>

    <button type="button" :disabled="ahorrado >= cantidadObjetivo" @click="emit('agregarAhorro')">
      Añadir 100 €
    </button>
  </article>
</template>

<style scoped>
.savings-goal {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding: 24px;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  background-color: #ffffff;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

h2 {
  margin: 0;
  color: #1f2937;
}

p {
  margin: 0;
  color: #4b5563;
}

progress {
  width: 100%;
  height: 16px;
  accent-color: #16a34a;
}

button {
  align-self: flex-start;
  margin-top: 16px;
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  background-color: #2563eb;
  color: white;
  cursor: pointer;
}

button:hover:not(:disabled) {
  background-color: #1d4ed8;
}

button:disabled {
  background-color: #9ca3af;
  cursor: not-allowed;
}
</style>
