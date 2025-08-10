<template>
  <div class="py-8 bg-gray-50 min-h-screen">
    <div class="max-w-8xl mx-auto px-6">
      <!-- Header -->
      <div class="mb-8">
        <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          Mano skydelis
        </h1>
        <p class="text-xl text-gray-600">
          Stebėkite savo investicijas ir grąžą
        </p>
      </div>

      <!-- Overview Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
        <div class="card p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600">Iš viso investuota</p>
              <p class="text-2xl font-bold text-gray-900">{{ formatCurrency(portfolio.totalInvested) }}</p>
            </div>
            <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center">
              <svg class="w-6 h-6 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"/>
              </svg>
            </div>
          </div>
        </div>

        <div class="card p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600">Uždirbtos palūkanos</p>
              <p class="text-2xl font-bold text-secondary-600">{{ formatCurrency(portfolio.earnedInterest) }}</p>
            </div>
            <div class="w-12 h-12 bg-secondary-100 rounded-lg flex items-center justify-center">
              <svg class="w-6 h-6 text-secondary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/>
              </svg>
            </div>
          </div>
        </div>

        <div class="card p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600">Aktyvūs projektai</p>
              <p class="text-2xl font-bold text-gray-900">{{ portfolio.activeProjects }}</p>
            </div>
            <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
              <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"/>
              </svg>
            </div>
          </div>
        </div>

        <div class="card p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-600">Piniginės likutis</p>
              <p class="text-2xl font-bold text-gray-900">{{ formatCurrency(portfolio.walletBalance) }}</p>
            </div>
            <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
              <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"/>
              </svg>
            </div>
          </div>
          <button 
            @click="showDepositModal = true"
            class="mt-4 w-full btn-secondary text-sm py-2"
          >
            Įnešti pinigų
          </button>
        </div>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Investment Portfolio -->
        <div class="lg:col-span-2">
          <div class="card">
            <div class="p-6 border-b border-gray-200">
              <h2 class="text-xl font-semibold text-gray-900">Mano investicijos</h2>
            </div>
            <div class="overflow-x-auto">
              <table class="w-full">
                <thead class="bg-gray-50">
                  <tr>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Projektas
                    </th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Investuota
                    </th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Palūkanos
                    </th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Terminas
                    </th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Būsena
                    </th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Uždirbta
                    </th>
                  </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                  <tr 
                    v-for="investment in portfolio.investments" 
                    :key="investment.id"
                    class="hover:bg-gray-50"
                  >
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div>
                        <div class="text-sm font-medium text-gray-900">{{ investment.projectTitle }}</div>
                        <div class="text-sm text-gray-500">Investuota: {{ formatDate(investment.investedDate) }}</div>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-gray-900">{{ formatCurrency(investment.amount) }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-secondary-600 font-medium">{{ investment.rate }}%</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-gray-900">{{ formatDate(investment.termEnd) }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <span 
                        :class="getStatusClass(investment.status)"
                        class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full"
                      >
                        {{ investment.status }}
                      </span>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-secondary-600 font-medium">{{ formatCurrency(investment.earnings) }}</div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- Wallet & Transactions -->
        <div class="lg:col-span-1">
          <!-- Wallet -->
          <div class="card p-6 mb-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">Piniginė</h3>
            <div class="space-y-4">
              <div class="flex justify-between items-center">
                <span class="text-gray-600">Dabartinis likutis</span>
                <span class="text-xl font-bold text-gray-900">{{ formatCurrency(portfolio.walletBalance) }}</span>
              </div>
              <div class="flex space-x-2">
                <button 
                  @click="showDepositModal = true"
                  class="flex-1 btn-secondary text-sm py-2"
                >
                  Įnešti
                </button>
                <button 
                  @click="showWithdrawModal = true"
                  class="flex-1 btn-outline text-sm py-2"
                  :disabled="portfolio.walletBalance <= 0"
                >
                  Išsiųsti
                </button>
              </div>
            </div>
          </div>

          <!-- Recent Transactions -->
          <div class="card p-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">Paskutiniai mokėjimai</h3>
            <div class="space-y-4">
              <div 
                v-for="transaction in recentTransactions" 
                :key="transaction.id"
                class="flex items-center justify-between py-2"
              >
                <div class="flex items-center space-x-3">
                  <div 
                    :class="getTransactionIconClass(transaction.type)"
                    class="w-8 h-8 rounded-full flex items-center justify-center"
                  >
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path 
                        v-if="transaction.type === 'deposit'"
                        stroke-linecap="round" 
                        stroke-linejoin="round" 
                        stroke-width="2" 
                        d="M12 6v6m0 0v6m0-6h6m-6 0H6"
                      />
                      <path 
                        v-else-if="transaction.type === 'withdrawal'"
                        stroke-linecap="round" 
                        stroke-linejoin="round" 
                        stroke-width="2" 
                        d="M20 12H4"
                      />
                      <path 
                        v-else-if="transaction.type === 'investment'"
                        stroke-linecap="round" 
                        stroke-linejoin="round" 
                        stroke-width="2" 
                        d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"
                      />
                      <path 
                        v-else
                        stroke-linecap="round" 
                        stroke-linejoin="round" 
                        stroke-width="2" 
                        d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"
                      />
                    </svg>
                  </div>
                  <div>
                    <div class="text-sm font-medium text-gray-900">{{ transaction.description }}</div>
                    <div class="text-xs text-gray-500">{{ formatDate(transaction.date) }}</div>
                  </div>
                </div>
                <div 
                  :class="transaction.amount > 0 ? 'text-green-600' : 'text-red-600'"
                  class="text-sm font-medium"
                >
                  {{ transaction.amount > 0 ? '+' : '' }}{{ formatCurrency(transaction.amount) }}
                </div>
              </div>
            </div>
            <div class="mt-4 pt-4 border-t border-gray-200">
              <button class="text-primary-600 hover:text-primary-800 text-sm font-medium">
                Peržiūrėti visus mokėjimus
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Deposit Modal -->
    <div v-if="showDepositModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto p-4 md:p-6 m-4">
        <div class="flex justify-between items-center mb-6">
          <h3 class="text-xl font-semibold text-gray-900">Įnešti pinigų</h3>
          <button @click="showDepositModal = false" class="text-gray-400 hover:text-gray-600">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>
        
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Suma (€)
            </label>
            <input 
              v-model.number="depositAmount" 
              type="number" 
              min="10" 
              step="10"
              class="input-field"
            />
          </div>
          
          <div class="bg-gray-50 rounded-lg p-4">
            <h4 class="font-medium text-gray-900 mb-2">SEPA pervedimo informacija</h4>
            <div class="space-y-2 text-sm">
              <div class="flex justify-between">
                <span class="text-gray-600">Gavėjas:</span>
                <span class="font-medium">Rontgen UAB</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">IBAN:</span>
                <span class="font-mono">LT12 1000 0111 0100 1000</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">SWIFT:</span>
                <span class="font-mono">EVIULT2X</span>
              </div>
            </div>
          </div>
          
          <div class="flex space-x-3">
            <button 
              @click="showDepositModal = false"
              class="flex-1 btn-outline"
            >
              Atšaukti
            </button>
            <button 
              @click="confirmDeposit"
              :disabled="depositAmount < 10"
              class="flex-1 btn-secondary disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Patvirtinti
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Withdraw Modal -->
    <div v-if="showWithdrawModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
      <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto p-4 md:p-6 m-4">
        <div class="flex justify-between items-center mb-6">
          <h3 class="text-xl font-semibold text-gray-900">Išsiųsti pinigus</h3>
          <button @click="showWithdrawModal = false" class="text-gray-400 hover:text-gray-600">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>
        
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              Suma (€)
            </label>
            <input 
              v-model.number="withdrawAmount" 
              type="number" 
              :min="10" 
              :max="portfolio.walletBalance"
              step="10"
              class="input-field"
            />
            <p class="text-xs text-gray-500 mt-1">
              Galima išsiųsti iki {{ formatCurrency(portfolio.walletBalance) }}
            </p>
          </div>
          
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">
              IBAN numeris
            </label>
            <input 
              v-model="withdrawIBAN" 
              type="text" 
              placeholder="LT12 1000 0111 0100 1000"
              class="input-field"
            />
          </div>
          
          <div class="flex space-x-3">
            <button 
              @click="showWithdrawModal = false"
              class="flex-1 btn-outline"
            >
              Atšaukti
            </button>
            <button 
              @click="confirmWithdraw"
              :disabled="withdrawAmount < 10 || withdrawAmount > portfolio.walletBalance || !withdrawIBAN"
              class="flex-1 btn-secondary disabled:opacity-50 disabled:cursor-not-allowed"
            >
              Patvirtinti
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { userPortfolio, transactions } from '../data/mockData.js'

const portfolio = ref(userPortfolio)
const showDepositModal = ref(false)
const showWithdrawModal = ref(false)
const depositAmount = ref(100)
const withdrawAmount = ref(100)
const withdrawIBAN = ref('')

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

const getStatusClass = (status) => {
  switch (status) {
    case 'Aktyvus':
      return 'bg-green-100 text-green-800'
    case 'Grąžintas':
      return 'bg-blue-100 text-blue-800'
    case 'Vėluoja':
      return 'bg-red-100 text-red-800'
    default:
      return 'bg-gray-100 text-gray-800'
  }
}

const getTransactionIconClass = (type) => {
  switch (type) {
    case 'deposit':
      return 'bg-green-100 text-green-600'
    case 'withdrawal':
      return 'bg-red-100 text-red-600'
    case 'investment':
      return 'bg-blue-100 text-blue-600'
    case 'interest':
      return 'bg-yellow-100 text-yellow-600'
    default:
      return 'bg-gray-100 text-gray-600'
  }
}

const recentTransactions = computed(() => {
  return transactions.slice(0, 5)
})

const confirmDeposit = () => {
  // Here you would typically make an API call
  alert(`Pervedimo informacija išsiųsta! Suma: ${formatCurrency(depositAmount.value)}`)
  showDepositModal.value = false
  depositAmount.value = 100
}

const confirmWithdraw = () => {
  // Here you would typically make an API call
  alert(`Išsiuntimo užklausa pateikta! Suma: ${formatCurrency(withdrawAmount.value)}`)
  showWithdrawModal.value = false
  withdrawAmount.value = 100
  withdrawIBAN.value = ''
}
</script>
