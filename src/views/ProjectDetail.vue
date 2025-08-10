<template>
  <div class="py-8 bg-gray-50 min-h-screen">
    <div class="max-w-8xl mx-auto px-6" v-if="project">
      <!-- Header -->
      <div class="mb-8">
        <nav class="flex items-center space-x-2 text-sm text-gray-600 mb-4">
          <router-link to="/projects" class="hover:text-primary-800">Projektai</router-link>
          <span>/</span>
          <span class="text-gray-900">{{ project.title }}</span>
        </nav>
        
        <div class="flex flex-col lg:flex-row justify-between items-start lg:items-center gap-4">
          <div class="flex-1 min-w-0">
            <h1 class="text-2xl md:text-3xl lg:text-4xl font-bold text-gray-900 mb-2">
              {{ project.title }}
            </h1>
            <p class="text-lg md:text-xl text-gray-600">{{ project.location }}</p>
          </div>
          <div class="flex items-center space-x-3 flex-shrink-0">
            <span class="bg-secondary-500 text-white px-3 md:px-4 py-2 rounded-full text-sm font-medium">
              {{ project.rating }}
            </span>
            <button 
              @click="showInvestmentModal = true"
              class="btn-secondary whitespace-nowrap"
              :disabled="project.status !== 'Atidarytas'"
            >
              Investuoti dabar
            </button>
          </div>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Main Content -->
        <div class="lg:col-span-2">
          <!-- Image Gallery -->
          <div class="card p-6 mb-8">
            <div class="relative mb-4">
              <img 
                :src="selectedImage" 
                :alt="project.title"
                class="w-full h-96 object-cover rounded-lg cursor-pointer"
                @click="showImageModal = true"
              />
            </div>
            <div class="grid grid-cols-4 gap-2">
              <img 
                v-for="(image, index) in project.images" 
                :key="index"
                :src="image" 
                :alt="`${project.title} - ${index + 1}`"
                class="w-full h-20 object-cover rounded cursor-pointer hover:opacity-80 transition-opacity"
                :class="{ 'ring-2 ring-primary-500': selectedImage === image }"
                @click="selectedImage = image"
              />
            </div>
          </div>

          <!-- Tabs -->
          <div class="card">
            <div class="border-b border-gray-200">
              <nav class="flex space-x-8 px-6">
                <button 
                  v-for="tab in tabs" 
                  :key="tab.id"
                  @click="activeTab = tab.id"
                  class="py-4 px-1 border-b-2 font-medium text-sm transition-colors duration-200"
                  :class="activeTab === tab.id 
                    ? 'border-primary-500 text-primary-600' 
                    : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'"
                >
                  {{ tab.name }}
                </button>
              </nav>
            </div>

            <div class="p-6">
              <!-- Overview Tab -->
              <div v-if="activeTab === 'overview'">
                <h3 class="text-xl font-semibold text-gray-900 mb-4">Projekto aprašymas</h3>
                <p class="text-gray-600 mb-6 leading-relaxed">{{ project.description }}</p>
                
                <h4 class="text-lg font-semibold text-gray-900 mb-3">Paskolos tikslas</h4>
                <p class="text-gray-600 mb-6">{{ project.purpose }}</p>
                
                <h4 class="text-lg font-semibold text-gray-900 mb-3">Statybininkas</h4>
                <p class="text-gray-600 mb-6">{{ project.developer }}</p>
                
                <h4 class="text-lg font-semibold text-gray-900 mb-3">Grąžinimo grafikas</h4>
                <div class="bg-gray-50 rounded-lg p-4">
                  <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
                    <div>
                      <div class="text-gray-600">Pradžios data</div>
                      <div class="font-semibold">2024 m. sausis</div>
                    </div>
                    <div>
                      <div class="text-gray-600">Pirmas mokėjimas</div>
                      <div class="font-semibold">2024 m. vasaris</div>
                    </div>
                    <div>
                      <div class="text-gray-600">Pabaigos data</div>
                      <div class="font-semibold">{{ getEndDate() }}</div>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Financials Tab -->
              <div v-if="activeTab === 'financials'">
                <h3 class="text-xl font-semibold text-gray-900 mb-4">Finansinė informacija</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                  <div class="card p-4">
                    <h4 class="font-semibold text-gray-900 mb-3">Paskolos informacija</h4>
                    <div class="space-y-2 text-sm">
                      <div class="flex justify-between">
                        <span class="text-gray-600">Paskolos suma:</span>
                        <span class="font-semibold">{{ formatCurrency(project.goal) }}</span>
                      </div>
                      <div class="flex justify-between">
                        <span class="text-gray-600">Palūkanų norma:</span>
                        <span class="font-semibold text-secondary-600">{{ project.rate }}%</span>
                      </div>
                      <div class="flex justify-between">
                        <span class="text-gray-600">Terminas:</span>
                        <span class="font-semibold">{{ project.term }} mėnesiai</span>
                      </div>
                      <div class="flex justify-between">
                        <span class="text-gray-600">Minimali investicija:</span>
                        <span class="font-semibold">{{ formatCurrency(project.minInvestment) }}</span>
                      </div>
                    </div>
                  </div>
                  
                  <div class="card p-4">
                    <h4 class="font-semibold text-gray-900 mb-3">Užtikrinimas</h4>
                    <div class="space-y-2 text-sm">
                      <div class="flex justify-between">
                        <span class="text-gray-600">Užtikrinimo tipas:</span>
                        <span class="font-semibold">{{ project.collateral }}</span>
                      </div>
                      <div class="flex justify-between">
                        <span class="text-gray-600">Turto vertė:</span>
                        <span class="font-semibold">{{ formatCurrency(project.valuation) }}</span>
                      </div>
                      <div class="flex justify-between">
                        <span class="text-gray-600">LTV santykis:</span>
                        <span class="font-semibold">{{ Math.round((project.goal / project.valuation) * 100) }}%</span>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Returns Calculator -->
                <div class="card p-6">
                  <h4 class="font-semibold text-gray-900 mb-4">Grąžos skaičiuoklė</h4>
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                      <label class="block text-sm font-medium text-gray-700 mb-2">
                        Investicijos suma (€)
                      </label>
                      <input 
                        v-model.number="calculatorAmount" 
                        type="number" 
                        min="100" 
                        step="100"
                        class="input-field"
                      />
                    </div>
                    <div class="bg-gray-50 rounded-lg p-4">
                      <div class="space-y-2 text-sm">
                        <div class="flex justify-between">
                          <span class="text-gray-600">Mėnesinės palūkanos:</span>
                          <span class="font-semibold">{{ formatCurrency(monthlyInterest) }}</span>
                        </div>
                        <div class="flex justify-between">
                          <span class="text-gray-600">Metinės palūkanos:</span>
                          <span class="font-semibold text-secondary-600">{{ formatCurrency(yearlyInterest) }}</span>
                        </div>
                        <div class="flex justify-between">
                          <span class="text-gray-600">Grąžinama suma:</span>
                          <span class="font-semibold">{{ formatCurrency(totalReturn) }}</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Documents Tab -->
              <div v-if="activeTab === 'documents'">
                <h3 class="text-xl font-semibold text-gray-900 mb-4">Dokumentai</h3>
                <div class="space-y-3">
                  <div 
                    v-for="doc in project.documents" 
                    :key="doc"
                    class="flex items-center justify-between p-4 border border-gray-200 rounded-lg hover:bg-gray-50 transition-colors"
                  >
                    <div class="flex items-center">
                      <svg class="w-8 h-8 text-red-500 mr-3" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd" d="M4 4a2 2 0 012-2h4.586A2 2 0 0112 2.586L15.414 6A2 2 0 0116 7.414V16a2 2 0 01-2 2H6a2 2 0 01-2-2V4zm2 6a1 1 0 011-1h6a1 1 0 110 2H7a1 1 0 01-1-1zm1 3a1 1 0 100 2h6a1 1 0 100-2H7z" clip-rule="evenodd"/>
                      </svg>
                      <span class="font-medium text-gray-900">{{ doc }}</span>
                    </div>
                    <button class="text-primary-600 hover:text-primary-800 font-medium">
                      Atsisiųsti
                    </button>
                  </div>
                </div>
              </div>

              <!-- Risks Tab -->
              <div v-if="activeTab === 'risks'">
                <h3 class="text-xl font-semibold text-gray-900 mb-4">Rizikos</h3>
                <div class="space-y-4">
                  <div 
                    v-for="(risk, index) in project.risks" 
                    :key="index"
                    class="flex items-start space-x-3 p-4 bg-yellow-50 border border-yellow-200 rounded-lg"
                  >
                    <svg class="w-5 h-5 text-yellow-600 mt-0.5 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"/>
                    </svg>
                    <span class="text-gray-700">{{ risk }}</span>
                  </div>
                </div>
              </div>

              <!-- Updates Tab -->
              <div v-if="activeTab === 'updates'">
                <h3 class="text-xl font-semibold text-gray-900 mb-4">Projekto atnaujinimai</h3>
                <div class="space-y-6">
                  <div 
                    v-for="update in project.updates" 
                    :key="update.date"
                    class="border-l-4 border-primary-500 pl-4"
                  >
                    <div class="flex items-center justify-between mb-2">
                      <h4 class="font-semibold text-gray-900">{{ update.title }}</h4>
                      <span class="text-sm text-gray-500">{{ formatDate(update.date) }}</span>
                    </div>
                    <p class="text-gray-600">{{ update.content }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Sidebar -->
        <div class="lg:col-span-1">
          <div class="sticky top-24">
            <!-- Key Facts -->
            <div class="card p-6 mb-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Pagrindinė informacija</h3>
              <div class="space-y-4">
                <div class="flex justify-between">
                  <span class="text-gray-600">Palūkanų norma</span>
                  <span class="font-semibold text-secondary-600">{{ project.rate }}%</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-gray-600">Terminas</span>
                  <span class="font-semibold">{{ project.term }} mėn.</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-gray-600">Užtikrinimas</span>
                  <span class="font-semibold">{{ project.collateral }}</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-gray-600">Min. investicija</span>
                  <span class="font-semibold">{{ formatCurrency(project.minInvestment) }}</span>
                </div>
              </div>
            </div>

            <!-- Funding Progress -->
            <div class="card p-6 mb-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Finansavimo progresas</h3>
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
              </div>
              <div class="grid grid-cols-2 gap-4 text-sm">
                <div>
                  <div class="text-gray-600">Surinkta</div>
                  <div class="font-semibold">{{ formatCurrency(project.funded) }}</div>
                </div>
                <div>
                  <div class="text-gray-600">Tikslas</div>
                  <div class="font-semibold">{{ formatCurrency(project.goal) }}</div>
                </div>
              </div>
              <div class="mt-4 pt-4 border-t border-gray-200">
                <div class="text-sm text-gray-600">
                  Liko {{ project.remainingDays }} dienų
                </div>
              </div>
            </div>

            <!-- Invest Button -->
            <button 
              @click="showInvestmentModal = true"
              class="btn-secondary w-full"
              :disabled="project.status !== 'Atidarytas'"
            >
              {{ project.status === 'Atidarytas' ? 'Investuoti dabar' : 'Projektas baigtas' }}
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Investment Modal -->
    <div v-if="showInvestmentModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto p-4 md:p-6 m-4">
        <div class="flex justify-between items-center mb-6">
          <h3 class="text-xl font-semibold text-gray-900">Investuoti į projektą</h3>
          <button @click="showInvestmentModal = false" class="text-gray-400 hover:text-gray-600">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>
        
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Investicijos suma (€)
            </label>
            <input 
              v-model.number="investmentAmount" 
              type="number" 
              :min="project.minInvestment" 
              :max="project.goal - project.funded"
              step="100"
              class="input-field"
            />
            <p class="text-xs text-gray-500 mt-1">
              Min: {{ formatCurrency(project.minInvestment) }}, 
              Max: {{ formatCurrency(project.goal - project.funded) }}
            </p>
          </div>
          
          <div class="bg-gray-50 rounded-lg p-4">
            <div class="space-y-2 text-sm">
              <div class="flex justify-between">
                <span class="text-gray-600">Mėnesinės palūkanos:</span>
                <span class="font-semibold">{{ formatCurrency(calculateMonthlyInterest(investmentAmount)) }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Metinės palūkanos:</span>
                <span class="font-semibold text-secondary-600">{{ formatCurrency(calculateYearlyInterest(investmentAmount)) }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">Grąžinama suma:</span>
                <span class="font-semibold">{{ formatCurrency(investmentAmount + calculateYearlyInterest(investmentAmount)) }}</span>
              </div>
            </div>
          </div>
          
          <label class="flex items-start space-x-3">
            <input 
              v-model="acceptTerms" 
              type="checkbox" 
              class="mt-1 rounded border-gray-300 text-primary-600 focus:ring-primary-500"
            />
            <span class="text-sm text-gray-600">
              Sutinku su <a href="#" class="text-primary-600 hover:text-primary-800">investicijos sąlygomis</a> 
              ir suprantu, kad investicijos nėra draudžiamos.
            </span>
          </label>
          
          <div class="flex space-x-3">
            <button 
              @click="showInvestmentModal = false"
              class="flex-1 btn-outline"
            >
              Atšaukti
            </button>
            <button 
              @click="confirmInvestment"
              :disabled="!acceptTerms || investmentAmount < project.minInvestment"
              class="flex-1 btn-secondary disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Patvirtinti investiciją
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Image Modal -->
    <div v-if="showImageModal" class="fixed inset-0 bg-black bg-opacity-90 flex items-center justify-center p-2 md:p-4 z-50">
      <div class="relative max-w-4xl w-full max-h-[90vh] overflow-hidden">
        <button @click="showImageModal = false" class="absolute top-4 right-4 text-white hover:text-gray-300 z-10">
          <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
        <img 
          :src="selectedImage" 
          :alt="project.title"
          class="w-full h-auto max-h-[85vh] object-contain"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { projects } from '../data/mockData.js'

const route = useRoute()
const router = useRouter()

const project = ref(null)
const selectedImage = ref('')
const activeTab = ref('overview')
const showInvestmentModal = ref(false)
const showImageModal = ref(false)
const investmentAmount = ref(100)
const acceptTerms = ref(false)
const calculatorAmount = ref(1000)

const tabs = [
  { id: 'overview', name: 'Apžvalga' },
  { id: 'financials', name: 'Finansai' },
  { id: 'documents', name: 'Dokumentai' },
  { id: 'risks', name: 'Rizikos' },
  { id: 'updates', name: 'Atnaujinimai' }
]

const formatCurrency = (amount) => {
  return new Intl.NumberFormat('lt-LT', {
    style: 'currency',
    currency: 'EUR',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(amount)
}

const formatDate = (dateString) => {
  return new Date(dateString).toLocaleDateString('lt-LT')
}

const getEndDate = () => {
  const startDate = new Date('2024-01-01')
  const endDate = new Date(startDate)
  endDate.setMonth(endDate.getMonth() + project.value.term)
  return endDate.toLocaleDateString('lt-LT', { year: 'numeric', month: 'long' })
}

const calculateMonthlyInterest = (amount) => {
  return (amount * project.value.rate / 100) / 12
}

const calculateYearlyInterest = (amount) => {
  return amount * project.value.rate / 100
}

const monthlyInterest = computed(() => calculateMonthlyInterest(calculatorAmount.value))
const yearlyInterest = computed(() => calculateYearlyInterest(calculatorAmount.value))
const totalReturn = computed(() => calculatorAmount.value + yearlyInterest.value)

const confirmInvestment = () => {
  // Here you would typically make an API call
  alert(`Investicija patvirtinta! Suma: ${formatCurrency(investmentAmount.value)}`)
  showInvestmentModal.value = false
  investmentAmount.value = 100
  acceptTerms.value = false
}

onMounted(() => {
  const projectId = parseInt(route.params.id)
  project.value = projects.find(p => p.id === projectId)
  
  if (!project.value) {
    router.push('/projects')
    return
  }
  
  selectedImage.value = project.value.images[0]
})
</script>
