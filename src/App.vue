<template>
  <div class="flex min-h-screen flex-col bg-slate-50 dark:bg-slate-950 text-slate-900 dark:text-slate-50 antialiased font-sans selection:bg-blue-500 selection:text-white transition-colors duration-300">
    
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute -top-[40%] -right-[60%] md:-top-[20%] md:-right-[20%] h-[600px] w-[600px] rounded-full bg-blue-400/10 dark:bg-blue-500/10 blur-[120px]"></div>
      <div class="absolute -bottom-[20%] -left-[20%] h-[500px] w-[500px] rounded-full bg-indigo-400/10 dark:bg-indigo-500/10 blur-[100px]"></div>
    </div>

    <div class="relative z-10 mx-auto flex w-full max-w-6xl flex-1 flex-col justify-between px-6 py-12 lg:px-12">
      
      <header class="flex items-center justify-between">
        <h1 class="text-xl font-extrabold tracking-tight select-none text-slate-900 dark:text-white">
          Project <span class="font-normal text-slate-500 dark:text-slate-400">TIOS</span>
        </h1>
        
        <div class="flex items-center gap-4">
          <button 
            @click="toggleTheme" 
            class="rounded-full p-2 text-slate-500 hover:bg-slate-200 dark:text-slate-400 dark:hover:bg-slate-800 transition-colors ring-1 ring-transparent focus:outline-none focus-visible:ring-blue-500"
            aria-label="Toggle Dark Mode"
          >
            <svg v-if="isDark" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
            <svg v-else class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
            </svg>
          </button>

          <div v-if="appVersion" class="inline-flex items-center gap-1.5 rounded-full bg-blue-50 dark:bg-blue-500/10 px-3 py-1 text-xs font-semibold text-blue-700 dark:text-blue-300 ring-1 ring-inset ring-blue-600/10 dark:ring-blue-500/20">
            <span class="h-1.5 w-1.5 rounded-full bg-blue-500 animate-pulse"></span>
            v{{ appVersion }}
          </div>
        </div>
      </header>

      <main class="grid grid-cols-1 gap-12 py-12 lg:grid-cols-12 lg:items-center lg:gap-16 lg:py-20">
        
        <div class="space-y-8 lg:col-span-7">
          <div class="space-y-4 text-center sm:text-left">
            <h2 class="text-4xl font-extrabold tracking-tight text-slate-900 dark:text-white sm:text-5xl lg:max-w-xl">
              Secure attendance tracking. <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600 dark:from-blue-400 dark:to-indigo-400">Simplified.</span>
            </h2>
            <p class="text-lg leading-relaxed text-slate-600 dark:text-slate-300 lg:max-w-lg mx-auto sm:mx-0">
              Empower your workspace with secure on-device biometric check-ins, custom access profile registrations, and real-time backend verification.
            </p>
          </div>

          <div class="flex flex-col items-center sm:items-start gap-3 w-full sm:w-auto min-h-[80px]">
            
            <div v-if="isLoading" class="flex items-center gap-3 text-slate-500 dark:text-slate-400 font-medium text-sm mt-3">
              <svg class="animate-spin h-5 w-5 text-blue-600 dark:text-blue-400" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              Reading configuration...
            </div>

            <div v-else-if="error" class="text-sm font-medium text-red-500 dark:text-red-400 mt-3 flex items-center gap-2">
              <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
              Could not load version data.
            </div>

            <div v-else class="w-full sm:w-auto space-y-4">
              <div class="flex flex-col sm:flex-row gap-3 w-full sm:w-auto">
                <!-- Android Download Button -->
                <a 
                  :href="apkDownloadUrl" 
                  download 
                  class="group flex items-center justify-center gap-2.5 rounded-xl bg-slate-900 dark:bg-white px-6 py-3.5 text-sm font-semibold text-white dark:text-slate-900 shadow-md shadow-slate-900/10 dark:shadow-white/10 transition-all hover:bg-slate-800 dark:hover:bg-slate-100 hover:shadow-lg active:scale-[0.98]"
                >
                  <svg class="h-5 w-5 fill-current" viewBox="0 0 24 24">
                    <path d="M17.523 15.3414c-.5511 0-.9993-.4486-.9993-.9997s.4482-.9993.9993-.9993c.552 0 .9997.4482.9997.9993s-.4477.9997-.9997.9997m-11.046 0c-.5511 0-.9993-.4486-.9993-.9997s.4482-.9993.9993-.9993c.552 0 .9997.4482.9997.9993s-.4477.9997-.9997.9997m11.4045-6.02l1.9973-3.4592c.1232-.2134.05-.4857-.1635-.6089-.2134-.1232-.4857-.05-.6089.1635l-2.0227 3.5032c-1.464-.6682-3.1362-1.0418-4.9127-1.0418s-3.4487.3736-4.9127 1.0418l-2.0227-3.5032c-.1232-.2135-.3955-.2867-.6089-.1635-.2135.1232-.2867.3955-.1635.6089l1.9973 3.4592c-3.1259 1.7018-5.2673 4.8814-5.4623 8.625h22.3426c-.195-3.7436-2.3364-6.9232-5.4623-8.625"/>
                  </svg>
                  Download APK
                </a>

                <!-- iOS Download Button -->
                <a 
                  :href="ipaDownloadUrl" 
                  download 
                  class="group flex items-center justify-center gap-2.5 rounded-xl bg-blue-600 dark:bg-blue-500 px-6 py-3.5 text-sm font-semibold text-white shadow-md shadow-blue-600/20 transition-all hover:bg-blue-700 dark:hover:bg-blue-600 hover:shadow-lg active:scale-[0.98]"
                >
                  <svg class="h-5 w-5 fill-current" viewBox="0 0 24 24">
                    <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 6.85c.66-.8 1.11-1.92.99-3.04-.96.04-2.13.64-2.82 1.44-.61.71-1.14 1.86-1 2.97 1.08.08 2.18-.57 2.83-1.37z"/>
                  </svg>
                  Download IPA
                </a>
              </div>

              <div class="flex flex-col sm:flex-row gap-2 sm:gap-6 text-xs text-slate-400 dark:text-slate-500 font-mono text-center sm:text-left justify-center sm:justify-start">
                <span v-if="apkFileName" class="truncate max-w-[200px]">APK: {{ apkFileName }}</span>
                <span v-if="ipaFileName" class="truncate max-w-[200px]">IPA: {{ ipaFileName }}</span>
              </div>
            </div>
          </div>
        </div>

        <div class="flex justify-center lg:col-span-5 w-full mt-6 lg:mt-0">
          <div class="relative w-[280px] h-[580px] sm:w-[320px] sm:h-[640px] rounded-[2.5rem] bg-slate-900 border-[6px] sm:border-[8px] border-slate-900 shadow-2xl ring-1 ring-black/20 dark:ring-white/10 transition-transform duration-500 hover:-translate-y-2">
            <div class="absolute -right-[10px] sm:-right-[12px] top-32 h-14 w-[4px] rounded-r-md bg-slate-800"></div> 
            <div class="absolute -left-[10px] sm:-left-[12px] top-24 h-10 w-[4px] rounded-l-md bg-slate-800"></div> 
            <div class="absolute -left-[10px] sm:-left-[12px] top-36 h-10 w-[4px] rounded-l-md bg-slate-800"></div> 
            <div class="relative flex w-full h-full overflow-x-auto overflow-y-hidden snap-x snap-mandatory rounded-[2rem] bg-slate-100 dark:bg-slate-950 [&::-webkit-scrollbar]:hidden [-ms-overflow-style:none] [scrollbar-width:none]">
              <img src="/01.jpg" alt="App Interface Screen 1" class="w-full h-full shrink-0 snap-center object-cover select-none pointer-events-none" />
              <img src="/02.png" alt="App Interface Screen 2" class="w-full h-full shrink-0 snap-center object-cover select-none pointer-events-none" />
              <img src="/03.png" alt="App Interface Screen 3" class="w-full h-full shrink-0 snap-center object-cover select-none pointer-events-none" />
            </div>
          </div>
        </div>
      </main>

      <footer class="flex flex-col gap-4 border-t border-slate-200/60 dark:border-slate-800/60 pt-8 sm:flex-row sm:items-center sm:justify-between text-xs text-slate-400 dark:text-slate-500 tracking-wide font-medium transition-colors text-center sm:text-left">
        <span>&copy; {{ new Date().getFullYear() }} Project TIOS Infrastructure.</span>
        <div class="flex justify-center sm:justify-start gap-6">
          <span class="hover:text-slate-600 dark:hover:text-slate-300 transition-colors">Enterprise Verified</span>
          <span class="hover:text-slate-600 dark:hover:text-slate-300 transition-colors">Android & iOS Builds</span>
        </div>
      </footer>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

// --- 1. TYPES ---
interface LocalVersionData {
  latest_version: string
  apk_download_url?: string
  ipa_download_url?: string
  download_url?: string // Fallback
}

// --- 2. REACTIVE STATE ---
const appVersion = ref<string>('')
const apkDownloadUrl = ref<string>('')
const ipaDownloadUrl = ref<string>('')
const apkFileName = ref<string>('')
const ipaFileName = ref<string>('')
const isLoading = ref<boolean>(true)
const error = ref<boolean>(false)

// Dark Mode State
const isDark = ref<boolean>(false)

// --- 3. LOGIC FUNCTIONS ---
const toggleTheme = (): void => {
  isDark.value = !isDark.value
  if (isDark.value) {
    document.documentElement.classList.add('dark')
    localStorage.setItem('theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    localStorage.setItem('theme', 'light')
  }
}

const fetchLocalConfig = async (): Promise<void> => {
  try {
    const response = await fetch(`${import.meta.env.BASE_URL}version.json`)
    if (!response.ok) throw new Error('Failed to fetch local configuration')

    const data: LocalVersionData = await response.json()
    
    appVersion.value = data.latest_version
    apkDownloadUrl.value = data.apk_download_url || data.download_url || '#'
    ipaDownloadUrl.value = data.ipa_download_url || '#'
    
    apkFileName.value = apkDownloadUrl.value !== '#' ? apkDownloadUrl.value.split('/').pop() || 'Project-TIOS.apk' : ''
    ipaFileName.value = ipaDownloadUrl.value !== '#' ? ipaDownloadUrl.value.split('/').pop() || 'Project-TIOS.ipa' : ''
    
  } catch (err) {
    console.error('Error reading version.json:', err)
    error.value = true
  } finally {
    isLoading.value = false
  }
}

// --- 4. LIFECYCLE HOOKS ---
onMounted((): void => {
  if (
    localStorage.getItem('theme') === 'dark' ||
    (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
  ) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  } else {
    isDark.value = false
    document.documentElement.classList.remove('dark')
  }

  fetchLocalConfig()
})
</script>