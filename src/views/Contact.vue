<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Hero Section -->
    <div class="bg-gradient-to-r from-primary-700 via-primary-600 to-primary-500 text-white py-16">
      <div class="max-w-8xl mx-auto px-6">
        <div class="text-center">
          <h1 class="text-4xl md:text-5xl font-bold mb-4">Susisiekite su mumis</h1>
          <p class="text-xl text-gray-100 max-w-2xl mx-auto">
            Turite klausimų apie investavimą? Esame čia, kad padėtume jums priimti geriausius sprendimus.
          </p>
        </div>
      </div>
    </div>

    <!-- Contact Content -->
    <div class="max-w-8xl mx-auto px-6 py-16">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <!-- Contact Form -->
        <div class="bg-white rounded-2xl shadow-lg p-8">
          <h2 class="text-2xl font-bold text-gray-900 mb-6">Siųskite mums žinutę</h2>
          
          <form @submit.prevent="submitForm" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label for="firstName" class="block text-sm font-medium text-gray-700 mb-2">
                  Vardas *
                </label>
                <input
                  id="firstName"
                  v-model="form.firstName"
                  type="text"
                  required
                  class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
                  placeholder="Jūsų vardas"
                />
              </div>
              
              <div>
                <label for="lastName" class="block text-sm font-medium text-gray-700 mb-2">
                  Pavardė *
                </label>
                <input
                  id="lastName"
                  v-model="form.lastName"
                  type="text"
                  required
                  class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
                  placeholder="Jūsų pavardė"
                />
              </div>
            </div>

            <div>
              <label for="email" class="block text-sm font-medium text-gray-700 mb-2">
                El. paštas *
              </label>
              <input
                id="email"
                v-model="form.email"
                type="email"
                required
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
                placeholder="jūsų@email.lt"
              />
            </div>

            <div>
              <label for="phone" class="block text-sm font-medium text-gray-700 mb-2">
                Telefono numeris
              </label>
              <input
                id="phone"
                v-model="form.phone"
                type="tel"
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
                placeholder="+370 6XX XXXXX"
              />
            </div>

            <div>
              <label for="subject" class="block text-sm font-medium text-gray-700 mb-2">
                Tema *
              </label>
              <select
                id="subject"
                v-model="form.subject"
                required
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
              >
                <option value="">Pasirinkite temą</option>
                <option value="investment">Investavimo klausimai</option>
                <option value="technical">Techninė pagalba</option>
                <option value="partnership">Bendradarbiavimas</option>
                <option value="general">Bendri klausimai</option>
                <option value="other">Kita</option>
              </select>
            </div>

            <div>
              <label for="message" class="block text-sm font-medium text-gray-700 mb-2">
                Žinutė *
              </label>
              <textarea
                id="message"
                v-model="form.message"
                rows="6"
                required
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200 resize-none"
                placeholder="Aprašykite savo klausimą ar pasiūlymą..."
              ></textarea>
            </div>

            <div class="flex items-start space-x-3">
              <input
                id="privacy"
                v-model="form.privacy"
                type="checkbox"
                required
                class="mt-1 h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
              />
              <label for="privacy" class="text-sm text-gray-600">
                Sutinku su <a href="#" class="text-primary-600 hover:text-primary-700 underline">privatumo politika</a> ir 
                <a href="#" class="text-primary-600 hover:text-primary-700 underline">naudojimo sąlygomis</a> *
              </label>
            </div>

            <button
              type="submit"
              :disabled="isSubmitting"
              class="w-full bg-primary-600 hover:bg-primary-700 disabled:bg-gray-400 text-white font-semibold py-3 px-6 rounded-lg transition-colors duration-200 flex items-center justify-center"
            >
              <svg v-if="isSubmitting" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              {{ isSubmitting ? 'Siunčiama...' : 'Siųsti žinutę' }}
            </button>
          </form>
        </div>

        <!-- Contact Information -->
        <div class="space-y-8">
          <!-- Company Info -->
          <div class="bg-white rounded-2xl shadow-lg p-8">
            <div class="flex items-center mb-6">
              <img src="https://rontgen.lt/lending/img/logo_white.png" alt="Rontgen" class="h-12 w-auto" />
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-4">Rontgen UAB</h3>
            <p class="text-gray-600 mb-6">
              Lietuvos nekilnojamojo turto investavimo platforma, padedanti investuotojams 
              pasiekti patikimus ir pelningus investavimo sprendimus.
            </p>
            
            <div class="space-y-4">
              <div class="flex items-start space-x-3">
                <div class="flex-shrink-0 w-6 h-6 bg-primary-100 rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                  </svg>
                </div>
                <div>
                  <p class="font-medium text-gray-900">Adresas</p>
                  <p class="text-gray-600">Gedimino pr. 1, Vilnius<br>LT-01103, Lietuva</p>
                </div>
              </div>

              <div class="flex items-start space-x-3">
                <div class="flex-shrink-0 w-6 h-6 bg-primary-100 rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
                  </svg>
                </div>
                <div>
                  <p class="font-medium text-gray-900">Telefonas</p>
                  <p class="text-gray-600">+370 5 212 3456</p>
                </div>
              </div>

              <div class="flex items-start space-x-3">
                <div class="flex-shrink-0 w-6 h-6 bg-primary-100 rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
                  </svg>
                </div>
                <div>
                  <p class="font-medium text-gray-900">El. paštas</p>
                  <p class="text-gray-600">info@rontgen.lt</p>
                </div>
              </div>

              <div class="flex items-start space-x-3">
                <div class="flex-shrink-0 w-6 h-6 bg-primary-100 rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                  </svg>
                </div>
                <div>
                  <p class="font-medium text-gray-900">Darbo laikas</p>
                  <p class="text-gray-600">Pirmadienis - Penktadienis: 9:00 - 18:00<br>Savaitgaliais: 10:00 - 16:00</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Trust Indicators -->
          <div class="bg-white rounded-2xl shadow-lg p-8">
            <h3 class="text-xl font-bold text-gray-900 mb-6">Mūsų patikimumas</h3>
            
            <div class="space-y-4">
              <div class="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                <div class="flex items-center space-x-3">
                  <svg class="w-8 h-8 text-yellow-500" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm0 22C6.486 22 2 17.514 2 12S6.486 2 12 2s10 4.486 10 10-4.486 10-10 10zm-1-6h2v2h-2v-2zm0-8h2v6h-2V8z"/>
                  </svg>
                  <div>
                    <p class="font-medium text-gray-900">Trustpilot reitingas</p>
                    <p class="text-sm text-gray-600">4.7/5 iš 500+ atsiliepimų</p>
                  </div>
                </div>
                <a href="https://www.trustpilot.com/review/rontgen.lt" target="_blank" class="text-primary-600 hover:text-primary-700 font-medium">
                  Peržiūrėti →
                </a>
              </div>

              <div class="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                <div class="flex items-center space-x-3">
                  <svg class="w-8 h-8 text-green-500" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
                  </svg>
                  <div>
                    <p class="font-medium text-gray-900">Licencija</p>
                    <p class="text-sm text-gray-600">Lietuvos banko licencija</p>
                  </div>
                </div>
                <span class="text-green-600 font-medium">Patvirtinta</span>
              </div>

              <div class="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                <div class="flex items-center space-x-3">
                  <svg class="w-8 h-8 text-blue-500" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"/>
                  </svg>
                  <div>
                    <p class="font-medium text-gray-900">Saugumas</p>
                    <p class="text-sm text-gray-600">SSL šifravimas ir KYC</p>
                  </div>
                </div>
                <span class="text-blue-600 font-medium">Apsaugota</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Map Section -->
    <div class="bg-gray-100 py-16">
      <div class="max-w-8xl mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold text-gray-900 mb-4">Mūsų biuras</h2>
          <p class="text-gray-600 max-w-2xl mx-auto">
            Apsilankykite mūsų biure Vilniuje, Gedimino prospekte. 
            Esame pasiruošę atsakyti į visus jūsų klausimus.
          </p>
        </div>
        
        <div class="bg-white rounded-2xl shadow-lg overflow-hidden">
          <div class="h-96 bg-gray-200 flex items-center justify-center">
            <div class="text-center">
              <svg class="w-16 h-16 text-gray-400 mx-auto mb-4" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 0C7.802 0 4 3.403 4 7.602C4 11.8 7.469 16.812 12 24C16.531 16.812 20 11.8 20 7.602C20 3.403 16.199 0 12 0ZM12 11C10.343 11 9 9.657 9 8C9 6.343 10.343 5 12 5C13.657 5 15 6.343 15 8C15 9.657 13.657 11 12 11Z"/>
              </svg>
              <p class="text-gray-500">Žemėlapis bus rodomas čia</p>
              <p class="text-sm text-gray-400">Gedimino pr. 1, Vilnius, Lietuva</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  subject: '',
  message: '',
  privacy: false
})

const isSubmitting = ref(false)

const submitForm = async () => {
  isSubmitting.value = true
  
  // Simulate form submission
  await new Promise(resolve => setTimeout(resolve, 2000))
  
  // Reset form
  form.value = {
    firstName: '',
    lastName: '',
    email: '',
    phone: '',
    subject: '',
    message: '',
    privacy: false
  }
  
  isSubmitting.value = false
  
  // Show success message (you can implement a toast notification here)
  alert('Ačiū! Jūsų žinutė buvo sėkmingai išsiųsta. Susisieksime su jumis netrukus.')
}
</script>
