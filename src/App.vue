<template>
  <div class="flex min-h-screen flex-col bg-slate-50 dark:bg-slate-950 text-slate-900 dark:text-slate-50 antialiased font-sans selection:bg-blue-500 selection:text-white transition-colors duration-300">
    
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute -top-[40%] -right-[60%] md:-top-[20%] md:-right-[20%] h-[600px] w-[600px] rounded-full bg-blue-400/10 dark:bg-blue-500/10 blur-[120px]"></div>
      <div class="absolute -bottom-[20%] -left-[20%] h-[500px] w-[500px] rounded-full bg-indigo-400/10 dark:bg-indigo-500/10 blur-[100px]"></div>
    </div>

    <div class="relative z-10 mx-auto flex w-full max-w-6xl flex-1 flex-col justify-between px-6 py-12 lg:px-12">
      
      <header class="flex items-center justify-between">
        <h1 class="text-xl font-extrabold tracking-tight select-none text-slate-900 dark:text-white">
          BMS<span class="font-normal text-slate-500 dark:text-slate-400">Mobile</span>
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

      <main class="grid grid-cols-1 gap-16 py-12 lg:grid-cols-12 lg:items-center lg:py-20">
        
        <div class="space-y-8 lg:col-span-7">
          <div class="space-y-4">
            <h2 class="text-4xl font-extrabold tracking-tight text-slate-900 dark:text-white sm:text-5xl lg:max-w-xl">
              Secure attendance tracking. <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600 dark:from-blue-400 dark:to-indigo-400">Simplified.</span>
            </h2>
            <p class="text-lg leading-relaxed text-slate-600 dark:text-slate-300 lg:max-w-lg">
              Empower your workspace with secure on-device biometric check-ins, custom access profile registrations, and real-time backend verification.
            </p>
          </div>

          <div class="inline-flex flex-col items-start gap-3 w-full sm:w-auto min-h-[80px]">
            
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

            <div v-else class="w-full sm:w-auto space-y-3">
              <a :href="downloadUrl" download class="group flex items-center justify-center gap-3 rounded-xl bg-slate-900 dark:bg-white px-8 py-3.5 text-base font-semibold text-white dark:text-slate-900 shadow-md shadow-slate-900/10 dark:shadow-white/10 transition-all hover:bg-slate-800 dark:hover:bg-slate-100 hover:shadow-lg hover:shadow-slate-900/20 dark:hover:shadow-white/20 active:scale-[0.98]">
                <svg class="h-5 w-5 text-slate-400 dark:text-slate-500 transition-transform group-hover:translate-y-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
                </svg>
                Download Official APK
              </a>
              <p class="text-xs text-slate-400 dark:text-slate-500 font-mono max-w-[280px] sm:max-w-sm truncate text-center sm:text-left">
                File: {{ fileName }}
              </p>
            </div>
          </div>
        </div>

        <div class="hidden lg:col-span-5 lg:flex lg:justify-center">
          <div class="relative w-[280px] h-[560px] rounded-[40px] bg-slate-900 p-3 shadow-2xl ring-1 ring-slate-900/10 dark:ring-white/10 transition-shadow">
            <div class="absolute top-5 left-1/2 h-4 w-24 -translate-x-1/2 rounded-full bg-slate-950 z-20"></div>
            
            <div class="relative h-full w-full overflow-hidden rounded-[32px] bg-slate-800">
              <img 
                src="/imagev2.jpg" 
                alt="App Interface" 
                class="h-full w-full object-cover select-none pointer-events-none"
              />
            </div>
          </div>
        </div>
      </main>

      <footer class="flex flex-col gap-4 border-t border-slate-200/60 dark:border-slate-800/60 pt-8 sm:flex-row sm:items-center sm:justify-between text-xs text-slate-400 dark:text-slate-500 tracking-wide font-medium transition-colors">
        <span>&copy; {{ new Date().getFullYear() }} BMS Technology Infrastructure.</span>
        <div class="flex gap-6">
          <span class="hover:text-slate-600 dark:hover:text-slate-300 transition-colors">Enterprise Verified</span>
          <span class="hover:text-slate-600 dark:hover:text-slate-300 transition-colors">Android Build</span>
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
  download_url: string
}

// --- 2. REACTIVE STATE ---
// App Data State
const appVersion = ref<string>('')
const downloadUrl = ref<string>('')
const fileName = ref<string>('')
const isLoading = ref<boolean>(true)
const error = ref<boolean>(false)

// Dark Mode State
const isDark = ref<boolean>(false)


// --- 3. LOGIC FUNCTIONS ---
// Toggle Dark Mode
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

// Fetch the JSON file from the public folder
const fetchLocalConfig = async (): Promise<void> => {
  try {
    const response = await fetch(`${import.meta.env.BASE_URL}version.json`)
    if (!response.ok) throw new Error('Failed to fetch local configuration')

    const data: LocalVersionData = await response.json()
    
    appVersion.value = data.latest_version
    downloadUrl.value = data.download_url
    
    // Extracts the filename automatically from the download_url
    fileName.value = data.download_url.split('/').pop() || 'application.apk'
    
  } catch (err) {
    console.error('Error reading version.json:', err)
    error.value = true
  } finally {
    isLoading.value = false
  }
}


// --- 4. LIFECYCLE HOOKS ---
onMounted((): void => {
  // A. Check local storage or system preference for Dark Mode on load
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

  // B. Fetch the version config
  fetchLocalConfig()
})
</script>