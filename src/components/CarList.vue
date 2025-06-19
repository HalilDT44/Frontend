<template>
  <div class="car-list">
    <div v-if="cars.length === 0" class="no-cars">
      <p>Keine Autos gefunden.</p>
    </div>
    <div v-else class="car-grid">
      <CarCard 
        v-for="car in cars" 
        :key="car.id"
        :car="car"
        @buy="$emit('buy', car)"
        @contact="$emit('contact', car)"
        @delete="$emit('delete', car)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import CarCard from './CarCard.vue'

interface Car {
  id: number
  brand: string
  model: string
  year: number
  price: number
  image: string
  description: string
}

interface Props {
  cars: Car[]
}

defineProps<Props>()
defineEmits<{
  buy: [car: Car]
  contact: [car: Car]
  delete: [car: Car]
}>()
</script>

<style scoped>
.car-list {
  width: 100%;
}

.car-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.no-cars {
  text-align: center;
  padding: 4rem 0;
  color: #6b7280;
  font-size: 1.125rem;
}

@media (max-width: 768px) {
  .car-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
}
</style>