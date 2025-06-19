<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="navbar-brand">
        <h2>AutoVerkauf</h2>
      </div>
      
      <div class="navbar-search">
        <input 
          type="text" 
          placeholder="Auto suchen..." 
          v-model="searchInput"
          @input="onSearch"
          class="search-input"
        >
        <button class="search-btn">🔍</button>
      </div>
      
      <div class="navbar-auth">
        <button 
          v-if="!isLoggedIn" 
          @click="$emit('login')"
          class="login-btn"
        >
          Anmelden
        </button>
        <div v-else class="user-menu">
          <span class="welcome-text">Willkommen!</span>
          <button 
            @click="$emit('logout')"
            class="logout-btn"
          >
            Abmelden
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  isLoggedIn: boolean
}

defineProps<Props>()

const emit = defineEmits<{
  search: [query: string]
  login: []
  logout: []
}>()

const searchInput = ref('')

const onSearch = () => {
  emit('search', searchInput.value)
}
</script>

<style scoped>
.navbar {
  background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 100;
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2rem;
}

.navbar-brand h2 {
  font-size: 1.5rem;
  font-weight: 700;
}

.navbar-search {
  display: flex;
  flex: 1;
  max-width: 400px;
  position: relative;
}

.search-input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: none;
  border-radius: 0.5rem 0 0 0.5rem;
  font-size: 1rem;
  outline: none;
}

.search-btn {
  padding: 0.75rem 1rem;
  background: #1e40af;
  color: white;
  border: none;
  border-radius: 0 0.5rem 0.5rem 0;
  cursor: pointer;
  transition: background-color 0.2s;
}

.search-btn:hover {
  background: #1e3a8a;
}

.navbar-auth {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.login-btn, .logout-btn {
  padding: 0.75rem 1.5rem;
  border: 2px solid white;
  background: transparent;
  color: white;
  border-radius: 0.5rem;
  cursor: pointer;
  font-weight: 500;
  transition: all 0.2s;
}

.login-btn:hover, .logout-btn:hover {
  background: white;
  color: #3b82f6;
}

.user-menu {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.welcome-text {
  font-weight: 500;
}

@media (max-width: 768px) {
  .navbar-container {
    flex-direction: column;
    gap: 1rem;
  }
  
  .navbar-search {
    max-width: 100%;
    width: 100%;
  }
  
  .navbar-brand h2 {
    font-size: 1.25rem;
  }
}
</style>