<template>
  <div class="min-h-screen bg-gray-50 flex flex-col justify-center py-12 sm:px-6 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-md">
      <div class="flex justify-center">
        <div class="w-12 h-12 bg-primary-800 rounded-lg flex items-center justify-center">
          <span class="text-white font-bold text-xl">N</span>
        </div>
      </div>
      <h2 class="mt-6 text-center text-3xl font-bold text-gray-900">
        Sukurti naują paskyrą
      </h2>
      <p class="mt-2 text-center text-sm text-gray-600">
        Arba
        <router-link to="/login" class="font-medium text-primary-600 hover:text-primary-500">
          prisijunkite prie esamos paskyros
        </router-link>
      </p>
    </div>

    <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md">
      <div class="card py-8 px-4 sm:px-10">
        <form class="space-y-6" @submit.prevent="handleRegister">
          <!-- Personal Information -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label for="firstName" class="block text-sm font-medium text-gray-700">
                Vardas
              </label>
              <div class="mt-1">
                <input
                  id="firstName"
                  v-model="form.firstName"
                  name="firstName"
                  type="text"
                  autocomplete="given-name"
                  required
                  class="input-field"
                  :class="{ 'border-red-500': errors.firstName }"
                  placeholder="Jonas"
                />
              </div>
              <p v-if="errors.firstName" class="mt-1 text-sm text-red-600">{{ errors.firstName }}</p>
            </div>

            <div>
              <label for="lastName" class="block text-sm font-medium text-gray-700">
                Pavardė
              </label>
              <div class="mt-1">
                <input
                  id="lastName"
                  v-model="form.lastName"
                  name="lastName"
                  type="text"
                  autocomplete="family-name"
                  required
                  class="input-field"
                  :class="{ 'border-red-500': errors.lastName }"
                  placeholder="Kazlauskas"
                />
              </div>
              <p v-if="errors.lastName" class="mt-1 text-sm text-red-600">{{ errors.lastName }}</p>
            </div>
          </div>

          <div>
            <label for="email" class="block text-sm font-medium text-gray-700">
              El. pašto adresas
            </label>
            <div class="mt-1">
              <input
                id="email"
                v-model="form.email"
                name="email"
                type="email"
                autocomplete="email"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.email }"
                placeholder="jusu@email.lt"
              />
            </div>
            <p v-if="errors.email" class="mt-1 text-sm text-red-600">{{ errors.email }}</p>
          </div>

          <div>
            <label for="phone" class="block text-sm font-medium text-gray-700">
              Telefono numeris
            </label>
            <div class="mt-1">
              <input
                id="phone"
                v-model="form.phone"
                name="phone"
                type="tel"
                autocomplete="tel"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.phone }"
                placeholder="+370 6XX XXXXX"
              />
            </div>
            <p v-if="errors.phone" class="mt-1 text-sm text-red-600">{{ errors.phone }}</p>
          </div>

          <div>
            <label for="personalCode" class="block text-sm font-medium text-gray-700">
              Asmens kodas
            </label>
            <div class="mt-1">
              <input
                id="personalCode"
                v-model="form.personalCode"
                name="personalCode"
                type="text"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.personalCode }"
                placeholder="12345678901"
                maxlength="11"
              />
            </div>
            <p v-if="errors.personalCode" class="mt-1 text-sm text-red-600">{{ errors.personalCode }}</p>
          </div>

          <!-- Address Information -->
          <div>
            <label for="address" class="block text-sm font-medium text-gray-700">
              Adresas
            </label>
            <div class="mt-1">
              <input
                id="address"
                v-model="form.address"
                name="address"
                type="text"
                autocomplete="street-address"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.address }"
                placeholder="Gedimino pr. 1, Vilnius"
              />
            </div>
            <p v-if="errors.address" class="mt-1 text-sm text-red-600">{{ errors.address }}</p>
          </div>

          <!-- Password -->
          <div>
            <label for="password" class="block text-sm font-medium text-gray-700">
              Slaptažodis
            </label>
            <div class="mt-1">
              <input
                id="password"
                v-model="form.password"
                name="password"
                type="password"
                autocomplete="new-password"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.password }"
                placeholder="••••••••"
              />
            </div>
            <p v-if="errors.password" class="mt-1 text-sm text-red-600">{{ errors.password }}</p>
          </div>

          <div>
            <label for="confirmPassword" class="block text-sm font-medium text-gray-700">
              Patvirtinti slaptažodį
            </label>
            <div class="mt-1">
              <input
                id="confirmPassword"
                v-model="form.confirmPassword"
                name="confirmPassword"
                type="password"
                autocomplete="new-password"
                required
                class="input-field"
                :class="{ 'border-red-500': errors.confirmPassword }"
                placeholder="••••••••"
              />
            </div>
            <p v-if="errors.confirmPassword" class="mt-1 text-sm text-red-600">{{ errors.confirmPassword }}</p>
          </div>

          <!-- Terms and Conditions -->
          <div class="space-y-4">
            <div class="flex items-start">
              <input
                id="terms"
                v-model="form.acceptTerms"
                name="terms"
                type="checkbox"
                required
                class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded mt-1"
              />
              <label for="terms" class="ml-2 block text-sm text-gray-900">
                Sutinku su 
                <a href="#" class="text-primary-600 hover:text-primary-500">naudojimo sąlygomis</a>
                ir 
                <a href="#" class="text-primary-600 hover:text-primary-500">privatumo politika</a>
              </label>
            </div>

            <div class="flex items-start">
              <input
                id="kyc"
                v-model="form.acceptKYC"
                name="kyc"
                type="checkbox"
                required
                class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded mt-1"
              />
              <label for="kyc" class="ml-2 block text-sm text-gray-900">
                Sutinku su KYC/AML procedūromis ir pateikti reikalingus dokumentus identifikacijai
              </label>
            </div>

            <div class="flex items-start">
              <input
                id="marketing"
                v-model="form.acceptMarketing"
                name="marketing"
                type="checkbox"
                class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded mt-1"
              />
              <label for="marketing" class="ml-2 block text-sm text-gray-900">
                Sutinku gauti rinkodaros pranešimus el. paštu
              </label>
            </div>
          </div>

          <div>
            <button
              type="submit"
              :disabled="loading"
              class="w-full btn-secondary disabled:opacity-50 disabled:cursor-not-allowed"
            >
              <span v-if="loading" class="flex items-center justify-center">
                <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                Registruojama...
              </span>
              <span v-else>Sukurti paskyrą</span>
            </button>
          </div>
        </form>

        <div class="mt-6">
          <div class="relative">
            <div class="absolute inset-0 flex items-center">
              <div class="w-full border-t border-gray-300" />
            </div>
            <div class="relative flex justify-center text-sm">
              <span class="px-2 bg-white text-gray-500">Arba registruokitės su</span>
            </div>
          </div>

          <div class="mt-6 grid grid-cols-2 gap-3">
            <button
              type="button"
              class="w-full inline-flex justify-center py-2 px-4 border border-gray-300 rounded-md shadow-sm bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
            >
              <svg class="w-5 h-5" viewBox="0 0 24 24">
                <path fill="currentColor" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                <path fill="currentColor" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                <path fill="currentColor" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                <path fill="currentColor" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
              </svg>
              <span class="ml-2">Google</span>
            </button>

            <button
              type="button"
              class="w-full inline-flex justify-center py-2 px-4 border border-gray-300 rounded-md shadow-sm bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
              </svg>
              <span class="ml-2">Facebook</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const loading = ref(false)

const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  personalCode: '',
  address: '',
  password: '',
  confirmPassword: '',
  acceptTerms: false,
  acceptKYC: false,
  acceptMarketing: false
})

const errors = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  personalCode: '',
  address: '',
  password: '',
  confirmPassword: ''
})

const validateForm = () => {
  // Clear previous errors
  Object.keys(errors).forEach(key => errors[key] = '')

  // First Name
  if (!form.firstName) {
    errors.firstName = 'Vardas yra privalomas'
  } else if (form.firstName.length < 2) {
    errors.firstName = 'Vardas turi būti bent 2 simbolių'
  }

  // Last Name
  if (!form.lastName) {
    errors.lastName = 'Pavardė yra privaloma'
  } else if (form.lastName.length < 2) {
    errors.lastName = 'Pavardė turi būti bent 2 simbolių'
  }

  // Email
  if (!form.email) {
    errors.email = 'El. pašto adresas yra privalomas'
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Įveskite teisingą el. pašto adresą'
  }

  // Phone
  if (!form.phone) {
    errors.phone = 'Telefono numeris yra privalomas'
  } else if (!/^\+370\s?\d{8}$/.test(form.phone.replace(/\s/g, ''))) {
    errors.phone = 'Įveskite teisingą lietuvišką telefono numerį'
  }

  // Personal Code
  if (!form.personalCode) {
    errors.personalCode = 'Asmens kodas yra privalomas'
  } else if (!/^\d{11}$/.test(form.personalCode)) {
    errors.personalCode = 'Asmens kodas turi būti 11 skaitmenų'
  }

  // Address
  if (!form.address) {
    errors.address = 'Adresas yra privalomas'
  }

  // Password
  if (!form.password) {
    errors.password = 'Slaptažodis yra privalomas'
  } else if (form.password.length < 8) {
    errors.password = 'Slaptažodis turi būti bent 8 simbolių'
  } else if (!/(?=.*[a-z])(?=.*[A-Z])(?=.*\d)/.test(form.password)) {
    errors.password = 'Slaptažodis turi turėti mažąją raidę, didžiąją raidę ir skaičių'
  }

  // Confirm Password
  if (!form.confirmPassword) {
    errors.confirmPassword = 'Patvirtinkite slaptažodį'
  } else if (form.password !== form.confirmPassword) {
    errors.confirmPassword = 'Slaptažodžiai nesutampa'
  }

  return !Object.values(errors).some(error => error)
}

const handleRegister = async () => {
  if (!validateForm()) return

  loading.value = true

  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // Mock successful registration
    localStorage.setItem('isAuthenticated', 'true')
    localStorage.setItem('user', JSON.stringify({
      id: 1,
      email: form.email,
      name: `${form.firstName} ${form.lastName}`,
      firstName: form.firstName,
      lastName: form.lastName
    }))
    
    alert('Paskyra sėkmingai sukurta! Dabar galite pradėti investuoti.')
    router.push('/dashboard')
  } catch (error) {
    console.error('Registration error:', error)
    alert('Registracijos klaida. Bandykite dar kartą.')
  } finally {
    loading.value = false
  }
}
</script>

