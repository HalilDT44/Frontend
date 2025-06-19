<template>
  <div id="app">
    <Navbar 
      @search="handleSearch" 
      @login="handleLogin"
      :isLoggedIn="isLoggedIn" 
      @logout="handleLogout"
    />
    <main class="main-content">
      <div class="container">
        <h1 class="page-title">Verfügbare Autos</h1>
        <CarList 
          :cars="filteredCars" 
          @buy="handleBuy"
          @contact="handleContact"
          @delete="handleDelete"
        />
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import Navbar from './components/Navbar.vue'
import CarList from './components/CarList.vue'

interface Car {
  id: number
  brand: string
  model: string
  year: number
  price: number
  image: string
  description: string
}

const isLoggedIn = ref(false)
const searchQuery = ref('')

// Mock-Daten - später durch API-Calls ersetzen
const cars = ref<Car[]>([
  {
    id: 1,
    brand: 'BMW',
    model: '320i',
    year: 2020,
    price: 35000,
    image: 'https://images.pexels.com/photos/3802510/pexels-photo-3802510.jpeg?auto=compress&cs=tinysrgb&w=600',
    description: 'Gepflegter BMW 320i mit geringer Laufleistung'
  },
  {
    id: 2,
    brand: 'Mercedes',
    model: 'C-Klasse',
    year: 2019,
    price: 32000,
    image: 'https://images.pexels.com/photos/116675/pexels-photo-116675.jpeg?auto=compress&cs=tinysrgb&w=600',
    description: 'Elegante Mercedes C-Klasse in sehr gutem Zustand'
  },
  {
    id: 3,
    brand: 'Audi',
    model: 'A4',
    year: 2021,
    price: 38000,
    image: 'https://images.pexels.com/photos/3422964/pexels-photo-3422964.jpeg?auto=compress&cs=tinysrgb&w=600',
    description: 'Sportlicher Audi A4 mit modernster Ausstattung'
  },
  {
    id: 4,
    brand: 'Volkswagen',
    model: 'Golf',
    year: 2020,
    price: 25000,
    image: 'https://images.pexels.com/photos/1335077/pexels-photo-1335077.jpeg?auto=compress&cs=tinysrgb&w=600',
    description: 'Zuverlässiger VW Golf - perfekt für die Stadt'
  }
])

const filteredCars = computed(() => {
  if (!searchQuery.value) return cars.value
  
  const query = searchQuery.value.toLowerCase()
  return cars.value.filter(car => 
    car.brand.toLowerCase().includes(query) ||
    car.model.toLowerCase().includes(query)
  )
})

const handleSearch = (query: string) => {
  searchQuery.value = query
}

const handleLogin = () => {
  isLoggedIn.value = !isLoggedIn.value
  if (isLoggedIn.value) {
    alert('Erfolgreich angemeldet!')
  }
}

const handleLogout = () => {
  isLoggedIn.value = false
  alert('Erfolgreich abgemeldet!')
}

const handleBuy = (car: Car) => {
  if (!isLoggedIn.value) {
    alert('Bitte melden Sie sich an, um ein Auto zu kaufen!')
    return
  }
  alert(`Auto ${car.brand} ${car.model} für ${car.price}€ gekauft!`)
  // Hier würde später der API-Call zum Backend kommen
}

const handleContact = (car: Car) => {
  alert(`Kontakt für ${car.brand} ${car.model} - Hier würde ein Kontaktformular geöffnet werden.`)
  // Hier würde später ein Kontaktformular oder Modal geöffnet werden
}

const handleDelete = (car: Car) => {
  if (!isLoggedIn.value) {
    alert('Bitte melden Sie sich an, um Autos zu löschen!')
    return
  }
  
  if (confirm(`Möchten Sie das Auto ${car.brand} ${car.model} wirklich löschen?`)) {
    const index = cars.value.findIndex(c => c.id === car.id)
    if (index > -1) {
      cars.value.splice(index, 1)
      alert('Auto erfolgreich gelöscht!')
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background-color: #f8fafc;
  color: #1f2937;
  line-height: 1.6;

}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.main-content {
  padding-top: 2rem;
  padding-bottom: 2rem;
}

.page-title {
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 3rem;
  color: #1f2937;
}

@media (max-width: 768px) {
  .page-title {
    font-size: 2rem;
    margin-bottom: 2rem;
  }
}
</style>