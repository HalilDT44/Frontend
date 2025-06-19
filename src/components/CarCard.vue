<template>
  <div class="car-card">
    <div class="car-image">
      <img :src="car.image" :alt="`${car.brand} ${car.model}`" />
    </div>
    
    <div class="car-content">
      <div class="car-header">
        <h3 class="car-title">{{ car.brand }} {{ car.model }}</h3>
        <span class="car-year">{{ car.year }}</span>
      </div>
      
      <p class="car-description">{{ car.description }}</p>
      
      <div class="car-price">
        <span class="price">{{ formatPrice(car.price) }}</span>
      </div>
      
      <div class="car-actions">
        <button @click="$emit('buy')" class="btn btn-primary">
          💰 Kaufen
        </button>
        <button @click="$emit('contact')" class="btn btn-secondary">
          📞 Kontakt
        </button>
        <button @click="$emit('delete')" class="btn btn-danger">
          🗑️ Löschen
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
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
  car: Car
}

defineProps<Props>()
defineEmits<{
  buy: []
  contact: []
  delete: []
}>()

const formatPrice = (price: number): string => {
  return new Intl.NumberFormat('de-DE', {
    style: 'currency',
    currency: 'EUR',
    minimumFractionDigits: 0
  }).format(price)
}
</script>

<style scoped>
.car-card {
  background: white;
  border-radius: 1rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: all 0.3s ease;
}

.car-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

.car-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.car-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.car-card:hover .car-image img {
  transform: scale(1.05);
}

.car-content {
  padding: 1.5rem;
}

.car-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.car-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1f2937;
}

.car-year {
  background: #e5e7eb;
  color: #6b7280;
  padding: 0.25rem 0.75rem;
  border-radius: 1rem;
  font-size: 0.875rem;
  font-weight: 500;
}

.car-description {
  color: #6b7280;
  margin-bottom: 1rem;
  line-height: 1.5;
}

.car-price {
  margin-bottom: 1.5rem;
}

.price {
  font-size: 1.5rem;
  font-weight: 700;
  color: #059669;
}

.car-actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.btn {
  flex: 1;
  min-width: 100px;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.5rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 0.875rem;
}

.btn-primary {
  background: #3b82f6;
  color: white;
}

.btn-primary:hover {
  background: #2563eb;
  transform: translateY(-1px);
}

.btn-secondary {
  background: #10b981;
  color: white;
}

.btn-secondary:hover {
  background: #059669;
  transform: translateY(-1px);
}

.btn-danger {
  background: #ef4444;
  color: white;
}

.btn-danger:hover {
  background: #dc2626;
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .car-actions {
    flex-direction: column;
  }
  
  .btn {
    flex: none;
  }
}
</style>