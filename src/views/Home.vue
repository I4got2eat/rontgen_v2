<template>
  <div>
    <!-- Hero Section -->
    <section class="relative bg-gradient-to-br from-primary-700 via-primary-600 to-primary-500 text-white overflow-hidden">
      <div class="absolute inset-0 bg-black opacity-20"></div>
      <div class="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1920&h=1080&fit=crop')] bg-cover bg-center opacity-10"></div>
      
      <div class="relative max-w-8xl mx-auto px-6 py-24 lg:py-32">
        <div class="max-w-4xl">
                     <h1 class="text-4xl md:text-6xl font-bold mb-6 leading-tight">
             Investuokite į nekilnojamąjį turtą nuo 100€
           </h1>
           <p class="text-xl md:text-2xl text-gray-200 mb-8 leading-relaxed">
             Investuokite į patikimus verslo paskolas, užtikrintas nekilnojamuoju turtu.
           </p>
          <div class="flex flex-col sm:flex-row gap-4">
            <button 
              @click="scrollToProjects"
              class="btn-secondary text-lg px-8 py-4"
            >
              Peržiūrėti projektus
            </button>
            <button class="btn-outline text-lg px-8 py-4 border-white text-white hover:bg-white hover:text-primary-800">
              Sužinoti daugiau
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Key Stats Strip -->
    <section class="bg-white py-16 border-b border-gray-200">
      <div class="max-w-8xl mx-auto px-6">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
          <div class="text-center">
            <div class="text-3xl md:text-4xl font-bold text-primary-600 mb-2">
              {{ formatCurrency(platformStats.totalInvested) }}
            </div>
            <div class="text-gray-600">Iš viso investuota</div>
          </div>
          <div class="text-center">
            <div class="text-3xl md:text-4xl font-bold text-primary-600 mb-2">
              {{ platformStats.investors.toLocaleString() }}+
            </div>
            <div class="text-gray-600">Investuotojų</div>
          </div>
          <div class="text-center">
            <div class="text-3xl md:text-4xl font-bold text-secondary-600 mb-2">
              {{ platformStats.avgReturn }}%
            </div>
            <div class="text-gray-600">Vidutinė grąža</div>
          </div>
          <div class="text-center">
            <div class="text-3xl md:text-4xl font-bold text-primary-600 mb-2">
              {{ platformStats.projectsRepaid.toLocaleString() }}
            </div>
            <div class="text-gray-600">Projektų grąžinta</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Featured Projects -->
    <section id="projects" class="py-16 bg-gray-50">
      <div class="max-w-8xl mx-auto px-6">
        <div class="text-center mb-12">
                     <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
             Populiariausi projektai
           </h2>
           <p class="text-xl text-gray-600 max-w-2xl mx-auto">
             Pasirinkite iš mūsų patikrintų ir hipoteka užtikrintų nekilnojamojo turto projektų
           </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="project in featuredProjects" 
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
            
            <router-link 
              :to="`/project/${project.id}`"
              class="btn-primary w-full text-center"
            >
              Investuoti dabar
            </router-link>
          </div>
        </div>
        
        <div class="text-center mt-12">
          <router-link to="/projects" class="btn-outline text-lg px-8 py-4">
            Peržiūrėti visus projektus
          </router-link>
        </div>
      </div>
    </section>

    <!-- How It Works -->
    <section class="py-16 bg-white">
      <div class="max-w-8xl mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
            Kaip tai veikia?
          </h2>
          <p class="text-xl text-gray-600 max-w-2xl mx-auto">
            Tik trys paprasti žingsniai iki jūsų pirmos investicijos
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="text-center">
            <div class="w-16 h-16 bg-primary-100 rounded-full flex items-center justify-center mx-auto mb-6">
              <span class="text-2xl font-bold text-primary-800">1</span>
            </div>
                         <h3 class="text-xl font-semibold text-gray-900 mb-4">Registruokitės ir patvirtinkite</h3>
             <p class="text-gray-600">
               Sukurkite paskyrą per kelias minutes ir pateikite reikalingus dokumentus 
               identifikacijai ir klientų pažinimo procedūrai.
             </p>
          </div>
          
          <div class="text-center">
            <div class="w-16 h-16 bg-primary-100 rounded-full flex items-center justify-center mx-auto mb-6">
              <span class="text-2xl font-bold text-primary-800">2</span>
            </div>
                         <h3 class="text-xl font-semibold text-gray-900 mb-4">Pasirinkite projektą</h3>
             <p class="text-gray-600">
               Peržiūrėkite mūsų patikrintus projektus ir pasirinkite tinkamiausią 
               pagal jūsų investavimo tikslus ir rizikos toleranciją.
             </p>
          </div>
          
          <div class="text-center">
            <div class="w-16 h-16 bg-primary-100 rounded-full flex items-center justify-center mx-auto mb-6">
              <span class="text-2xl font-bold text-primary-800">3</span>
            </div>
                         <h3 class="text-xl font-semibold text-gray-900 mb-4">Gaukite palūkanas ir grąžą</h3>
             <p class="text-gray-600">
               Investuokite nuo 100€ ir pradėkite gauti mėnesines palūkanas. 
               Pasibaigus terminui, grąžinama visa investuota suma.
             </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Trustpilot Section -->
    <section class="py-16 bg-white">
      <div class="max-w-8xl mx-auto px-6">
        <div class="text-center mb-12">
                     <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
             Mūsų investuotojai mus vertina
           </h2>
           <p class="text-xl text-gray-600 max-w-2xl mx-auto">
             Sužinokite, kodėl tūkstančiai investuotojų pasirinko Rontgen platformą
           </p>
        </div>

                          <div class="bg-gradient-to-r from-green-50 to-green-100 rounded-2xl p-8 md:p-12">
           <div class="text-center max-w-4xl mx-auto">
             <div class="bg-gradient-to-r from-green-600 to-green-700 rounded-xl p-6 mb-6 inline-block">
               <img src="https://cdn.trustpilot.net/brand-assets/4.3.0/logo-white.svg" alt="Trustpilot" class="h-12 w-auto" />
             </div>
             
             <div class="flex items-center justify-center mb-6">
               <div class="flex text-yellow-400 mr-4">
                 <svg v-for="star in 5" :key="star" class="w-8 h-8 relative" fill="currentColor" viewBox="0 0 20 20">
                   <defs>
                     <linearGradient id="starGradient">
                       <stop offset="0%" stop-color="#FCD34D" />
                       <stop offset="94%" stop-color="#FCD34D" />
                       <stop offset="94%" stop-color="#D1D5DB" />
                       <stop offset="100%" stop-color="#D1D5DB" />
                     </linearGradient>
                   </defs>
                   <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" fill="url(#starGradient)" />
                 </svg>
               </div>
               <div>
                 <div class="text-3xl font-bold text-gray-900">4.7/5</div>
                 <div class="text-gray-600">iš 500+ atsiliepimų</div>
               </div>
             </div>
             
                           <p class="text-gray-700 mb-8 text-lg max-w-2xl mx-auto">
                "Puiki platforma investavimui! Aiškūs projektai, greitas procesas ir puiki klientų aptarnavimo komanda. Rekomenduoju visiems, kurie nori investuoti į nekilnojamąjį turtą."
              </p>
             
             <a 
               href="https://www.trustpilot.com/review/rontgen.lt" 
               target="_blank"
               class="inline-flex items-center bg-green-600 hover:bg-green-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors duration-200"
             >
               Peržiūrėti visus atsiliepimus
               <svg class="w-5 h-5 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                 <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/>
               </svg>
             </a>
           </div>
         </div>
      </div>
    </section>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { projects, testimonials, platformStats } from '../data/mockData.js'

const featuredProjects = ref(projects.slice(0, 6))

const formatCurrency = (amount) => {
  return new Intl.NumberFormat('lt-LT', {
    style: 'currency',
    currency: 'EUR',
    minimumFractionDigits: 0,
    maximumFractionDigits: 0
  }).format(amount)
}

const scrollToProjects = () => {
  const element = document.getElementById('projects')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>
