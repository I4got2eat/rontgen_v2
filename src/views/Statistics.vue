<template>
  <div class="py-8 bg-gray-50 min-h-screen">
    <div class="max-w-8xl mx-auto px-6">
      <!-- Header -->
      <div class="text-center mb-12">
        <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          Platformos statistika
        </h1>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Realaus laiko duomenys apie Rontgen platformos veiklą ir investuotojų rezultatus
        </p>
      </div>

      <!-- Key Metrics -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-12">
        <div class="card p-6 text-center">
          <div class="text-3xl font-bold text-primary-600 mb-2">
            {{ formatCurrency(platformStats.totalInvested) }}
          </div>
          <div class="text-gray-600">Iš viso investuota</div>
          <div class="text-sm text-green-600 mt-2">+12.5% šį mėnesį</div>
        </div>

        <div class="card p-6 text-center">
          <div class="text-3xl font-bold text-primary-600 mb-2">
            {{ platformStats.investors.toLocaleString() }}+
          </div>
          <div class="text-gray-600">Aktyvūs investuotojai</div>
          <div class="text-sm text-green-600 mt-2">+156 šį mėnesį</div>
        </div>

        <div class="card p-6 text-center">
          <div class="text-3xl font-bold text-secondary-600 mb-2">
            {{ platformStats.avgReturn }}%
          </div>
          <div class="text-gray-600">Vidutinė grąža</div>
          <div class="text-sm text-green-600 mt-2">+0.3% šį mėnesį</div>
        </div>

        <div class="card p-6 text-center">
          <div class="text-3xl font-bold text-primary-600 mb-2">
            {{ platformStats.projectsRepaid.toLocaleString() }}
          </div>
          <div class="text-gray-600">Sėkmingai grąžinti projektai</div>
          <div class="text-sm text-green-600 mt-2">+8 šį mėnesį</div>
        </div>
      </div>

      <!-- Detailed Statistics -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Platform Performance -->
        <div class="card p-6">
          <h2 class="text-xl font-semibold text-gray-900 mb-6">Platformos veikla</h2>
          <div class="space-y-4">
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Aktyvūs projektai</span>
              <span class="font-semibold">24</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Vidutinis projekto dydis</span>
              <span class="font-semibold">{{ formatCurrency(450000) }}</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Vidutinis finansavimo laikas</span>
              <span class="font-semibold">2.3 valandos</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Vėluojančių projektų</span>
              <span class="font-semibold text-red-600">1 (0.8%)</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Sėkmingai grąžintų</span>
              <span class="font-semibold text-green-600">99.2%</span>
            </div>
          </div>
        </div>

        <!-- Investor Demographics -->
        <div class="card p-6">
          <h2 class="text-xl font-semibold text-gray-900 mb-6">Investuotojų demografija</h2>
          <div class="space-y-4">
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Vidutinis investuotojas</span>
              <span class="font-semibold">{{ formatCurrency(8500) }}</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Didžiausia investicija</span>
              <span class="font-semibold">{{ formatCurrency(150000) }}</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Aktyvūs investuotojai</span>
              <span class="font-semibold">18,456</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Nauji investuotojai (šį mėn.)</span>
              <span class="font-semibold text-green-600">+1,234</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600">Išlaikymo laikas</span>
              <span class="font-semibold">14.2 mėn.</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Project Categories -->
      <div class="card p-6 mb-12">
        <h2 class="text-xl font-semibold text-gray-900 mb-6">Projektų kategorijos</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="text-center">
            <div class="w-16 h-16 bg-primary-100 rounded-full flex items-center justify-center mx-auto mb-4">
              <svg class="w-8 h-8 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"/>
              </svg>
            </div>
            <h3 class="font-semibold text-gray-900 mb-2">Gyvenamasis turtas</h3>
            <div class="text-2xl font-bold text-primary-600 mb-1">68%</div>
            <div class="text-sm text-gray-600">{{ formatCurrency(148000000) }}</div>
          </div>

          <div class="text-center">
            <div class="w-16 h-16 bg-secondary-100 rounded-full flex items-center justify-center mx-auto mb-4">
              <svg class="w-8 h-8 text-secondary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2-2v2m8 0V6a2 2 0 012 2v6a2 2 0 01-2 2H8a2 2 0 01-2-2V8a2 2 0 012-2V6"/>
              </svg>
            </div>
            <h3 class="font-semibold text-gray-900 mb-2">Komercijos turtas</h3>
            <div class="text-2xl font-bold text-secondary-600 mb-1">24%</div>
            <div class="text-sm text-gray-600">{{ formatCurrency(52000000) }}</div>
          </div>

          <div class="text-center">
            <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
              <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
              </svg>
            </div>
            <h3 class="font-semibold text-gray-900 mb-2">Energetikos projektai</h3>
            <div class="text-2xl font-bold text-green-600 mb-1">8%</div>
            <div class="text-sm text-gray-600">{{ formatCurrency(19000000) }}</div>
          </div>
        </div>
      </div>

      <!-- Monthly Performance -->
      <div class="card p-6 mb-12">
        <h2 class="text-xl font-semibold text-gray-900 mb-6">Mėnesinė veikla</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div class="text-center">
            <div class="text-2xl font-bold text-primary-600 mb-1">€12.4M</div>
            <div class="text-sm text-gray-600">Naujos investicijos</div>
            <div class="text-xs text-green-600 mt-1">+8.2% vs praėjusį mėn.</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-secondary-600 mb-1">€1.2M</div>
            <div class="text-sm text-gray-600">Išmokėtos palūkanos</div>
            <div class="text-xs text-green-600 mt-1">+5.1% vs praėjusį mėn.</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-green-600 mb-1">156</div>
            <div class="text-sm text-gray-600">Nauji investuotojai</div>
            <div class="text-xs text-green-600 mt-1">+12.3% vs praėjusį mėn.</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-blue-600 mb-1">8</div>
            <div class="text-sm text-gray-600">Baigti projektai</div>
            <div class="text-xs text-green-600 mt-1">+14.3% vs praėjusį mėn.</div>
          </div>
        </div>
      </div>

      <!-- Risk Metrics -->
      <div class="card p-6">
        <h2 class="text-xl font-semibold text-gray-900 mb-6">Rizikos metrika</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="text-center">
            <div class="text-2xl font-bold text-green-600 mb-1">99.2%</div>
            <div class="text-sm text-gray-600">Sėkmingai grąžintų projektų</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-yellow-600 mb-1">0.6%</div>
            <div class="text-sm text-gray-600">Vėluojančių projektų</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-red-600 mb-1">0.2%</div>
            <div class="text-sm text-gray-600">Problematinių projektų</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { platformStats } from '../data/mockData.js'

const formatCurrency = (amount) => {
  return new Intl.NumberFormat('lt-LT', {
    style: 'currency',
    currency: 'EUR',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(amount)
}
</script>

