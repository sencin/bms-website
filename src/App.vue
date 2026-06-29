<template>
  <div class="flex min-h-screen flex-col bg-slate-50 text-slate-900 antialiased font-sans selection:bg-blue-500 selection:text-white">
    
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute -top-[40%] -right-[60%] md:-top-[20%] md:-right-[20%] h-[600px] w-[600px] rounded-full bg-blue-400/10 blur-[120px]"></div>
      <div class="absolute -bottom-[20%] -left-[20%] h-[500px] w-[500px] rounded-full bg-indigo-400/10 blur-[100px]"></div>
    </div>

    <div class="relative z-10 mx-auto flex w-full max-w-6xl flex-1 flex-col justify-between px-6 py-12 lg:px-12">
      
      <header class="flex items-center justify-between">
        <h1 class="text-xl font-extrabold tracking-tight select-none">
          BMS<span class="font-normal text-slate-500">Mobile</span>
        </h1>
        <div v-if="appVersion" class="inline-flex items-center gap-1.5 rounded-full bg-blue-50 px-3 py-1 text-xs font-semibold text-blue-700 ring-1 ring-inset ring-blue-600/10">
          <span class="h-1.5 w-1.5 rounded-full bg-blue-500 animate-pulse"></span>
          v{{ appVersion }}
        </div>
      </header>

      <main class="grid grid-cols-1 gap-16 py-12 lg:grid-cols-12 lg:items-center lg:py-20">
        
        <div class="space-y-8 lg:col-span-7">
          <div class="space-y-4">
            <h2 class="text-4xl font-extrabold tracking-tight text-slate-900 sm:text-5xl lg:max-w-xl">
              Secure attendance tracking. <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600">Simplified.</span>
            </h2>
            <p class="text-lg leading-relaxed text-slate-600 lg:max-w-lg">
              Empower your workspace with secure on-device biometric check-ins, custom access profile registrations, and real-time backend verification.
            </p>
          </div>

          <div class="inline-flex flex-col items-start gap-3 w-full sm:w-auto min-h-[80px]">
            
            <div v-if="isLoading" class="flex items-center gap-3 text-slate-500 font-medium text-sm mt-3">
              <svg class="animate-spin h-5 w-5 text-blue-600" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              Reading configuration...
            </div>

            <div v-else-if="error" class="text-sm font-medium text-red-500 mt-3 flex items-center gap-2">
              <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
              Could not load version data.
            </div>

            <div v-else class="w-full sm:w-auto space-y-3">
              <a :href="downloadUrl" download class="group flex items-center justify-center gap-3 rounded-xl bg-slate-900 px-8 py-3.5 text-base font-semibold text-white shadow-md shadow-slate-900/10 transition-all hover:bg-slate-800 hover:shadow-lg hover:shadow-slate-900/20 active:scale-[0.98]">
                <svg class="h-5 w-5 text-slate-400 transition-transform group-hover:translate-y-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
                </svg>
                Download Official APK
              </a>
              <p class="text-xs text-slate-400 font-mono max-w-[280px] sm:max-w-sm truncate text-center sm:text-left">
                File: {{ fileName }}
              </p>
            </div>
          </div>
        </div>

        <div class="hidden lg:col-span-5 lg:flex lg:justify-center">
          <div class="relative w-[280px] h-[560px] rounded-[40px] bg-slate-900 p-3 shadow-2xl ring-1 ring-slate-900/10">
            <div class="absolute top-5 left-1/2 h-4 w-24 -translate-x-1/2 rounded-full bg-slate-950 z-20"></div>
            <div class="relative h-full w-full overflow-hidden rounded-[32px] bg-gradient-to-b from-slate-950 via-slate-900 to-slate-950 border border-slate-800 flex flex-col justify-between p-6 text-center select-none">
              <div class="mt-16 space-y-2">
                <div class="mx-auto h-12 w-12 rounded-2xl bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-blue-400 font-extrabold text-sm">
                  BMS
                </div>
                <h3 class="text-xs font-bold text-slate-400 uppercase tracking-widest mt-2">Mobile Profile</h3>
                <div class="mx-auto w-24 h-1.5 rounded-full bg-slate-800"></div>
              </div>
              
              <div class="my-auto flex justify-center opacity-20">
                <div class="relative flex items-center justify-center h-28 w-28 rounded-full border border-dashed border-blue-400 animate-[spin_40s_linear_infinite]">
                  <div class="h-20 w-20 rounded-full border border-solid border-indigo-400"></div>
                  <div class="absolute h-10 w-10 rounded-full bg-blue-500/30 blur-md"></div>
                </div>
              </div>

              <div class="mb-4 space-y-2">
                <div class="h-8 w-full rounded-xl bg-slate-800/50 border border-slate-800/40"></div>
                <div class="h-8 w-full rounded-xl bg-blue-600/30 border border-blue-500/20"></div>
              </div>
            </div>
          </div>
        </div>
      </main>

      <footer class="flex flex-col gap-4 border-t border-slate-200/60 pt-8 sm:flex-row sm:items-center sm:justify-between text-xs text-slate-400 tracking-wide font-medium">
        <span>&copy; {{ new Date().getFullYear() }} BMS Technology Infrastructure.</span>
        <div class="flex gap-6">
          <span class="hover:text-slate-600">Enterprise Verified</span>
          <span class="hover:text-slate-600">Android Build</span>
        </div>
      </footer>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

// Interface to match the structure of our version.json
interface LocalVersionData {
  latest_version: string
  download_url: string
}

// Reactive state variables
const appVersion = ref<string>('')
const downloadUrl = ref<string>('')
const fileName = ref<string>('')
const isLoading = ref<boolean>(true)
const error = ref<boolean>(false)

// Fetch the JSON file from the public folder when the page loads
const fetchLocalConfig = async (): Promise<void> => {
  try {
    const response = await fetch(`${import.meta.env.BASE_URL}version.json`)
    if (!response.ok) throw new Error('Failed to fetch local configuration')

    const data: LocalVersionData = await response.json()
    
    appVersion.value = data.latest_version
    downloadUrl.value = data.download_url
    
    // Extracts the filename automatically from the download_url (e.g., "app-release.apk")
    fileName.value = data.download_url.split('/').pop() || 'application.apk'
    
  } catch (err) {
    console.error('Error reading version.json:', err)
    error.value = true
  } finally {
    isLoading.value = false
  }
}

onMounted((): void => {
  fetchLocalConfig()
})
</script>