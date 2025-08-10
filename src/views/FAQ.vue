<template>
  <div class="py-8 bg-gray-50 min-h-screen">
    <div class="max-w-8xl mx-auto px-6">
      <!-- Header -->
      <div class="text-center mb-12">
        <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
          Dažnai užduodami klausimai
        </h1>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Atsakymai į dažniausiai užduodamus klausimus apie investavimą per Rontgen platformą
        </p>
      </div>

      <!-- FAQ Sections -->
      <div class="max-w-4xl mx-auto">
        <!-- General Questions -->
        <div class="mb-12">
          <h2 class="text-2xl font-bold text-gray-900 mb-6">Bendri klausimai</h2>
          <div class="space-y-4">
            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kas yra Rontgen platforma?
              </h3>
              <p class="text-gray-600">
                Rontgen yra Lietuvos banko reguliuojama crowdfunding platforma, siūlanti investicijas į nekilnojamąjį turtą, 
                aviaciją ir energetikos projektus. Mūsų pagrindinės vertybės yra skaidrumas ir konservatyvumas.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kokia minimali investicijos suma?
              </h3>
              <p class="text-gray-600">
                Minimali investicijos suma yra 100€. Galite investuoti bet kokią sumą, kuri yra 100€ kartotinis.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Ar investicijos yra draudžiamos?
              </h3>
              <p class="text-gray-600">
                Ne, investicijos nėra draudžiamos. Tai reiškia, kad jūsų investicijos nėra apsaugotos valstybės 
                draudimo sistemos. Ankstesni rezultatai negarantuoja ateities grąžos.
              </p>
            </div>
          </div>
        </div>

        <!-- Investment Process -->
        <div class="mb-12">
          <h2 class="text-2xl font-bold text-gray-900 mb-6">Investavimo procesas</h2>
          <div class="space-y-4">
            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kaip pradėti investuoti?
              </h3>
              <p class="text-gray-600">
                1. Registruokitės platformoje<br>
                2. Pateikite KYC dokumentus identifikacijai<br>
                3. Įneškite pinigų į savo piniginę<br>
                4. Pasirinkite projektą ir investuokite
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kokie dokumentai reikalingi registracijai?
              </h3>
              <p class="text-gray-600">
                Reikalingi: asmens tapatybės dokumentas, adreso patvirtinimas, pajamų šaltinių patvirtinimas. 
                Visi dokumentai turi būti teisėtai legalizuoti.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kaip veikia palūkanų mokėjimas?
              </h3>
              <p class="text-gray-600">
                Palūkanos mokamos mėnesiškai tiesiogiai į jūsų banko sąskaitą. Mokėjimai atliekami automatiškai 
                kiekvieno mėnesio pirmą dieną.
              </p>
            </div>
          </div>
        </div>

        <!-- Security & Risks -->
        <div class="mb-12">
          <h2 class="text-2xl font-bold text-gray-900 mb-6">Saugumas ir rizika</h2>
          <div class="space-y-4">
            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Ar mano pinigai yra saugūs?
              </h3>
              <p class="text-gray-600">
                Taip, visi projektai yra užtikrinti pirmuoju hipotekos rangu. Tai reiškia, kad jei paskolos gavėjas 
                negali grąžinti paskolos, mes galime realizuoti užstatą ir grąžinti jūsų investiciją.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kokia yra investavimo rizika?
              </h3>
              <p class="text-gray-600">
                Nors visi projektai yra kruopščiai atrinkti, investavimas visada turi riziką. Galimi rizikos veiksniai: 
                statybos vėlavimas, rinkos sąlygų pokyčiai, ekonomikos nuosmukis.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Ar galima anksčiau išsiųsti investiciją?
              </h3>
              <p class="text-gray-600">
                Standartiniu atveju investicijos negalima išsiųsti anksčiau nei pasibaigus terminui. Tačiau kai kuriais 
                atvejais galimas anksčiau grąžinimas, jei projektas grąžina paskolą anksčiau.
              </p>
            </div>
          </div>
        </div>

        <!-- Platform Features -->
        <div class="mb-12">
          <h2 class="text-2xl font-bold text-gray-900 mb-6">Platformos funkcijos</h2>
          <div class="space-y-4">
            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kaip sekti savo investicijas?
              </h3>
              <p class="text-gray-600">
                Prisijungę prie savo paskyros galite matyti visas savo investicijas, gautas palūkanas ir projekto 
                atnaujinimus realiu laiku.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Ar galima investuoti į kelis projektus?
              </h3>
              <p class="text-gray-600">
                Taip, galite investuoti į kiekvieną norimą projektą. Rekomenduojame diversifikuoti investicijas 
                į kelis projektus, kad sumažintumėte riziką.
              </p>
            </div>

            <div class="card p-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-2">
                Kokie yra platformos mokesčiai?
              </h3>
              <p class="text-gray-600">
                Platforma neima jokių mokesčių iš investuotojų. Visos palūkanos mokamos jums pilnai. 
                Vienintelis mokestis gali būti banko pervedimo mokestis.
              </p>
            </div>
          </div>
        </div>

        <!-- Contact Support -->
        <div class="text-center">
          <div class="card p-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">
              Neradote atsakymo?
            </h3>
            <p class="text-gray-600 mb-6">
              Jei turite papildomų klausimų, susisiekite su mūsų klientų aptarnavimo komanda
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center">
              <a href="mailto:info@rontgen.lt" class="btn-primary">
                Parašyti el. laišką
              </a>
              <a href="tel:+37068234551" class="btn-outline">
                Paskambinti +370 682 34551
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// No additional logic needed for FAQ page
</script>
