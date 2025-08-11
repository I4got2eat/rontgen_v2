<script setup>
import { ref } from 'vue'

const mobileMenuOpen = ref(false)
</script>

<template>
  <div id="app" class="min-h-screen bg-gray-50">
    <!-- Navigation Header -->
    <nav class="bg-primary-700 shadow-lg sticky top-0 z-50 transition-all duration-300 sticky">
      <div class="max-w-8xl mx-auto px-6">
        <div class="flex justify-between items-center h-16">
          <!-- Logo -->
          <router-link to="/" class="flex items-center flex-shrink-0">
            <img src="https://rontgen.lt/lending/img/logo_white.png" alt="Rontgen" class="h-8 md:h-10 w-auto" />
          </router-link>

          <!-- Desktop Navigation -->
          <div class="hidden md:flex items-center space-x-8">
            <router-link 
              to="/projects" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
            >
              Investuoti
            </router-link>
            <router-link 
              to="/how-it-works" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
            >
              Kaip veikia
            </router-link>
            <router-link 
              to="/statistics" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
            >
              Statistika
            </router-link>
            <router-link 
              to="/faq" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
            >
              DUK
            </router-link>
          </div>

          <!-- Auth Buttons -->
          <div class="hidden md:flex items-center space-x-4">
            <router-link 
              to="/login" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
            >
              Prisijungti
            </router-link>
            <router-link 
              to="/register" 
              class="btn-secondary"
            >
              Registruotis
            </router-link>
          </div>

          <!-- Mobile menu button -->
          <button 
            @click="mobileMenuOpen = !mobileMenuOpen"
            class="md:hidden p-2 rounded-md text-gray-300 hover:text-white hover:bg-gray-800 ml-4 flex-shrink-0"
            aria-label="Atidaryti meniu"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>

        <!-- Mobile Navigation -->
        <div v-if="mobileMenuOpen" class="md:hidden py-4 border-t border-primary-600">
          <div class="flex flex-col space-y-4">
            <router-link 
              to="/projects" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
              @click="mobileMenuOpen = false"
            >
              Investuoti
            </router-link>
            <router-link 
              to="/how-it-works" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
              @click="mobileMenuOpen = false"
            >
              Kaip veikia
            </router-link>
            <router-link 
              to="/statistics" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
              @click="mobileMenuOpen = false"
            >
              Statistika
            </router-link>
            <router-link 
              to="/faq" 
              class="text-gray-300 hover:text-white font-medium transition-colors duration-200"
              @click="mobileMenuOpen = false"
            >
              DUK
            </router-link>
            <div class="pt-4 border-t border-primary-600">
              <router-link 
                to="/login" 
                class="block text-gray-300 hover:text-white font-medium transition-colors duration-200 mb-2"
                @click="mobileMenuOpen = false"
              >
                Prisijungti
              </router-link>
              <router-link 
                to="/register" 
                class="btn-secondary inline-block"
                @click="mobileMenuOpen = false"
              >
                Registruotis
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <main>
      <router-view />
    </main>

    <!-- Footer -->
    <footer class="bg-primary-700 text-white py-12">
      <div class="max-w-8xl mx-auto px-6">
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-8">
          <!-- Company Info -->
          <div class="lg:col-span-2">
            <div class="flex items-center mb-4">
              <img src="https://rontgen.lt/lending/img/logo_white.png" alt="Rontgen" class="h-10 w-auto" />
            </div>
            <p class="text-gray-200 mb-4 leading-relaxed">
              Investuokite į nekilnojamąjį turtą vos nuo 100€. Visi projektai yra patikrinti, 
              hipoteka užtikrinti ir aiškūs.
            </p>
            <div class="flex space-x-4">
              <a href="#" class="text-gray-200 hover:text-white transition-colors duration-200">
                <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M22.46 6c-.77.35-1.6.58-2.46.69.88-.53 1.56-1.37 1.88-2.38-.83.5-1.75.85-2.72 1.05C18.37 4.5 17.26 4 16 4c-2.35 0-4.27 1.92-4.27 4.29 0 .34.04.67.11.98C8.28 9.09 5.11 7.38 3 4.79c-.37.63-.58 1.37-.58 2.15 0 1.49.75 2.81 1.91 3.56-.71 0-1.37-.2-1.95-.5v.03c0 2.08 1.48 3.82 3.44 4.21a4.22 4.22 0 0 1-1.93.07 4.28 4.28 0 0 0 4 2.98 8.521 8.521 0 0 1-5.33 1.84c-.34 0-.68-.02-1.02-.06C3.44 20.29 5.7 21 8.12 21 16 21 20.33 14.46 20.33 8.79c0-.19 0-.37-.01-.56.84-.6 1.56-1.36 2.14-2.23z"/>
                </svg>
              </a>
              <a href="#" class="text-gray-200 hover:text-white transition-colors duration-200">
                <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div class="lg:col-span-1">
            <h3 class="text-lg font-semibold mb-4">Nuorodos</h3>
            <ul class="space-y-2">
              <li><router-link to="/how-it-works" class="text-gray-200 hover:text-white transition-colors duration-200">Kaip tai veikia</router-link></li>
              <li><router-link to="/statistics" class="text-gray-200 hover:text-white transition-colors duration-200 font-semibold text-primary-300">Statistika</router-link></li>
              <li><router-link to="/faq" class="text-gray-200 hover:text-white transition-colors duration-200">DUK</router-link></li>
              <li><router-link to="/contact" class="text-gray-200 hover:text-white transition-colors duration-200">Kontaktai</router-link></li>
            </ul>
          </div>

          <!-- Contact -->
          <div class="lg:col-span-1">
            <h3 class="text-lg font-semibold mb-4">Kontaktai</h3>
            <ul class="space-y-2 text-gray-200">
              <li>info@rontgen.lt</li>
              <li>+370 5 212 3456</li>
              <li>Vilnius, Lietuva</li>
            </ul>
          </div>
        </div>

        <div class="border-t border-primary-600 mt-8 pt-8 text-center text-gray-200">
          <p class="text-sm">
            Investicijos nėra draudžiamos. Ankstesni rezultatai negarantuoja ateities grąžos. 
            © 2025 Rontgen UAB. Visos teisės saugomos.
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
