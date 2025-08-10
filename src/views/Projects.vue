<template>
  <div class="py-8 bg-gray-50 min-h-screen">
    <div class="max-w-8xl mx-auto px-6">
      <!-- Header -->
      <div class="mb-8">
        <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          Investicijos projektai
        </h1>
        <p class="text-xl text-gray-600">
          Pasirinkite iš mūsų patikrintų nekilnojamojo turto projektų
        </p>
      </div>

      <div class="flex flex-col lg:flex-row gap-8">
        <!-- Filters Sidebar -->
        <div class="lg:w-80 flex-shrink-0">
          <div class="card p-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-6">Filtrai</h3>
            
            <!-- Interest Rate Range -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-3">
                Palūkanų norma ({{ interestRange[0] }}% - {{ interestRange[1] }}%)
              </label>
              <div class="space-y-2">
                <input 
                  v-model="interestRange[0]" 
                  type="range" 
                  min="5" 
                  max="15" 
                  step="0.5"
                  class="w-full"
                />
                <input 
                  v-model="interestRange[1]" 
                  type="range" 
                  min="5" 
                  max="15" 
                  step="0.5"
                  class="w-full"
                />
              </div>
            </div>

            <!-- Term Length -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-3">Termino ilgis</label>
              <div class="space-y-2">
                <label class="flex items-center">
                  <input 
                    v-model="selectedTerms" 
                    type="checkbox" 
                    value="short"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">&lt; 6 mėnesių</span>
                </label>
                <label class="flex items-center">
                  <input 
                    v-model="selectedTerms" 
                    type="checkbox" 
                    value="medium"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">6-12 mėnesių</span>
                </label>
                <label class="flex items-center">
                  <input 
                    v-model="selectedTerms" 
                    type="checkbox" 
                    value="long"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">&gt; 12 mėnesių</span>
                </label>
              </div>
            </div>

            <!-- Risk Rating -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-3">Rizikos reitingas</label>
              <div class="space-y-2">
                <label 
                  v-for="rating in ['A+', 'A', 'B+', 'B', 'C']" 
                  :key="rating"
                  class="flex items-center"
                >
                  <input 
                    v-model="selectedRatings" 
                    type="checkbox" 
                    :value="rating"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">{{ rating }}</span>
                </label>
              </div>
            </div>

            <!-- Funding Status -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-3">Finansavimo būsena</label>
              <div class="space-y-2">
                <label class="flex items-center">
                  <input 
                    v-model="selectedStatuses" 
                    type="checkbox" 
                    value="Atidarytas"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">Atidarytas</span>
                </label>
                <label class="flex items-center">
                  <input 
                    v-model="selectedStatuses" 
                    type="checkbox" 
                    value="Pilnai finansuotas"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">Pilnai finansuotas</span>
                </label>
                <label class="flex items-center">
                  <input 
                    v-model="selectedStatuses" 
                    type="checkbox" 
                    value="Baigtas"
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                  <span class="ml-2 text-sm text-gray-700">Baigtas</span>
                </label>
              </div>
            </div>

            <!-- Location -->
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-3">Vieta</label>
              <select 
                v-model="selectedLocation"
                class="input-field"
              >
                <option value="">Visos vietos</option>
                <option value="Vilnius">Vilnius</option>
                <option value="Kaunas">Kaunas</option>
                <option value="Klaipėda">Klaipėda</option>
                <option value="Šiauliai">Šiauliai</option>
              </select>
            </div>

            <!-- Reset Filters -->
            <button 
              @click="resetFilters"
              class="w-full btn-outline"
            >
              Išvalyti filtrus
            </button>
          </div>
        </div>

        <!-- Projects Grid -->
        <div class="flex-1">
          <!-- Sort and Results -->
          <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6">
            <div class="text-gray-600 mb-4 sm:mb-0">
              Rasta {{ filteredProjects.length }} projektų
            </div>
            <div class="flex items-center space-x-4">
              <label class="text-sm font-medium text-gray-700">Rūšiuoti pagal:</label>
              <select 
                v-model="sortBy"
                class="input-field w-auto"
              >
                <option value="newest">Naujausius</option>
                <option value="rate">Palūkanų normą</option>
                <option value="term">Terminą</option>
                <option value="progress">Finansavimo progresą</option>
              </select>
            </div>
          </div>

          <!-- Projects Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
            <div 
              v-for="project in sortedProjects" 
              :key="project.id"
              class="card p-6"
            >
              <div class="relative mb-4">
                <img 
                  :src="project.images[0]" 
                  :alt="project.title"
                  class="w-full h-48 object-cover rounded-lg"
                />
                <div class="absolute top-3 left-3">
                  <span class="bg-secondary-500 text-white px-3 py-1 rounded-full text-sm font-medium">
                    {{ project.rating }}
                  </span>
                </div>
                <div class="absolute top-3 right-3">
                  <span 
                    :class="getStatusClass(project.status)"
                    class="px-3 py-1 rounded-full text-sm font-medium"
                  >
                    {{ project.status }}
                  </span>
                </div>
              </div>
              
              <h3 class="text-xl font-semibold text-gray-900 mb-2">{{ project.title }}</h3>
              <p class="text-gray-600 mb-4">{{ project.location }}</p>
              
              <div class="mb-4">
                <div class="flex justify-between text-sm text-gray-600 mb-2">
                  <span>Finansuota</span>
                  <span>{{ Math.round((project.funded / project.goal) * 100) }}%</span>
                </div>
                <div class="progress-bar">
                  <div 
                    class="progress-fill" 
                    :style="{ width: (project.funded / project.goal) * 100 + '%' }"
                  ></div>
                </div>
                <div class="text-xs text-gray-500 mt-1">
                  {{ formatCurrency(project.funded) }} / {{ formatCurrency(project.goal) }}
                </div>
              </div>
              
              <div class="grid grid-cols-3 gap-4 mb-6 text-sm">
                <div>
                  <div class="text-gray-600">Palūkanos</div>
                  <div class="font-semibold text-secondary-600">{{ project.rate }}%</div>
                </div>
                <div>
                  <div class="text-gray-600">Terminas</div>
                  <div class="font-semibold">{{ project.term }} mėn.</div>
                </div>
                <div>
                  <div class="text-gray-600">Min. invest.</div>
                  <div class="font-semibold">{{ formatCurrency(project.minInvestment) }}</div>
                </div>
              </div>
              
              <div class="flex items-center justify-between mb-4">
                <div class="text-sm text-gray-600">
                  Liko {{ project.remainingDays }} dienų
                </div>
                <div class="text-sm text-gray-600">
                  {{ formatCurrency(project.valuation) }}
                </div>
              </div>
              
              <router-link 
                :to="`/project/${project.id}`"
                class="btn-primary w-full text-center"
              >
                Peržiūrėti projektą
              </router-link>
            </div>
          </div>

          <!-- No Results -->
          <div v-if="filteredProjects.length === 0" class="text-center py-12">
            <div class="text-gray-500 text-lg mb-4">
              Nerasta projektų pagal pasirinktus filtrus
            </div>
            <button 
              @click="resetFilters"
              class="btn-outline"
            >
              Išvalyti filtrus
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { projects } from '../data/mockData.js'

// Filters
const interestRange = ref([5, 15])
const selectedTerms = ref([])
const selectedRatings = ref([])
const selectedStatuses = ref([])
const selectedLocation = ref('')
const sortBy = ref('newest')

const formatCurrency = (amount) => {
  return new Intl.NumberFormat('lt-LT', {
    style: 'currency',
    currency: 'EUR',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(amount)
}

const getStatusClass = (status) => {
  switch (status) {
    case 'Atidarytas':
      return 'bg-green-100 text-green-800'
    case 'Pilnai finansuotas':
      return 'bg-blue-100 text-blue-800'
    case 'Baigtas':
      return 'bg-gray-100 text-gray-800'
    default:
      return 'bg-gray-100 text-gray-800'
  }
}

const filteredProjects = computed(() => {
  return projects.filter(project => {
    // Interest rate filter
    if (project.rate < interestRange.value[0] || project.rate > interestRange.value[1]) {
      return false
    }

    // Term filter
    if (selectedTerms.value.length > 0) {
      const term = project.term
      const hasMatchingTerm = selectedTerms.value.some(selectedTerm => {
        switch (selectedTerm) {
          case 'short':
            return term < 6
          case 'medium':
            return term >= 6 && term <= 12
          case 'long':
            return term > 12
          default:
            return false
        }
      })
      if (!hasMatchingTerm) return false
    }

    // Rating filter
    if (selectedRatings.value.length > 0 && !selectedRatings.value.includes(project.rating)) {
      return false
    }

    // Status filter
    if (selectedStatuses.value.length > 0 && !selectedStatuses.value.includes(project.status)) {
      return false
    }

    // Location filter
    if (selectedLocation.value && !project.location.includes(selectedLocation.value)) {
      return false
    }

    return true
  })
})

const sortedProjects = computed(() => {
  const projects = [...filteredProjects.value]
  
  switch (sortBy.value) {
    case 'rate':
      return projects.sort((a, b) => b.rate - a.rate)
    case 'term':
      return projects.sort((a, b) => a.term - b.term)
    case 'progress':
      return projects.sort((a, b) => (b.funded / b.goal) - (a.funded / a.goal))
    case 'newest':
    default:
      return projects.sort((a, b) => b.id - a.id)
  }
})

const resetFilters = () => {
  interestRange.value = [5, 15]
  selectedTerms.value = []
  selectedRatings.value = []
  selectedStatuses.value = []
  selectedLocation.value = ''
  sortBy.value = 'newest'
}
</script>
