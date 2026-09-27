<template>
  <div :class="{ dark: isDarkMode }">
    <div
      class="flex h-screen bg-white text-gray-900 dark:bg-[#121212] dark:text-white font-sans overflow-hidden transition-colors duration-300 relative"
    >
      <aside
        class="w-64 bg-gray-50 border-r border-gray-200 dark:bg-[#181818] dark:border-gray-800 flex flex-col p-6 transition-colors duration-300 z-10"
      >
        <div class="text-2xl font-bold mb-10 flex items-center gap-3">
          <span
            class="bg-orange-500 text-white rounded-full w-8 h-8 flex items-center justify-center text-sm shadow-md shrink-0"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path
                fill-rule="evenodd"
                d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10ZM12 15a3 3 0 1 0 0-6 3 3 0 0 0 0 6Z"
                clip-rule="evenodd"
              />
            </svg>
          </span>
          SpoJeDy
        </div>

        <nav class="flex-1 space-y-6">
          <button
            @click="halamanAktif = 'home'"
            :class="
              halamanAktif === 'home'
                ? 'text-orange-500 font-bold'
                : 'text-gray-600 dark:text-gray-400 hover:text-orange-500'
            "
            class="flex items-center gap-4 font-semibold transition-colors w-full text-left"
          >
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />
            </svg>
            Home
          </button>

          <button
            @click="halamanAktif = 'mv'"
            :class="
              halamanAktif === 'mv'
                ? 'text-orange-500 font-bold'
                : 'text-gray-600 dark:text-gray-400 hover:text-orange-500'
            "
            class="flex items-center gap-4 font-semibold transition-colors w-full text-left"
          >
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M17 10.5V7c0-.55-.45-1-1-1H4c-.55 0-1 .45-1 1v10c0 .55.45 1 1 1h12c.55 0 1-.45 1-1v-3.5l4 4v-11l-4 4z"
              />
            </svg>
            Music Video
          </button>

          <button
            @click="halamanAktif = 'profile'"
            :class="
              halamanAktif === 'profile'
                ? 'text-orange-500 font-bold'
                : 'text-gray-600 dark:text-gray-400 hover:text-orange-500'
            "
            class="flex items-center gap-4 font-semibold transition-colors w-full text-left"
          >
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"
              />
            </svg>
            Profile
          </button>
        </nav>

        <div
          class="mt-auto flex items-center gap-3 pt-6 border-t border-gray-200 dark:border-gray-800 transition-colors duration-300"
        >
          <img
            :src="
              username && !fotoProfil
                ? 'https://ui-avatars.com/api/?name=' + username + '&background=f97316&color=fff'
                : fotoProfil
            "
            alt="Profile"
            class="w-10 h-10 rounded-full object-cover"
          />
          <div class="flex flex-col truncate">
            <span class="font-medium text-sm truncate">{{ username }}</span>
          </div>
        </div>
      </aside>

      <main
        class="flex-1 p-8 overflow-y-auto bg-gradient-to-b from-orange-100 to-white dark:from-[#282828] dark:to-[#121212] transition-colors duration-300"
      >
        <div v-if="halamanAktif === 'home'">
          <header class="mb-8 mt-4 flex flex-col gap-1">
            <h1 class="text-4xl font-extrabold tracking-tight">Hello, {{ username }}.</h1>
            <p class="text-xl font-medium text-gray-500 dark:text-gray-400 mt-2">
              What do you want to listen to today?
            </p>
          </header>

          <section>
            <h2 class="text-2xl font-bold mb-6">Top Songs For You</h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
              <div
                v-for="song in daftarLagu"
                :key="song.id"
                @click="bukaDetailLagu(song)"
                class="bg-white dark:bg-[#181818] p-4 rounded-xl hover:bg-orange-50 dark:hover:bg-[#282828] shadow-sm hover:shadow-md dark:shadow-none transition duration-300 cursor-pointer group border border-gray-100 dark:border-transparent"
              >
                <div
                  class="relative mb-4 rounded-xl p-3 transition-colors duration-300 group-hover:bg-orange-100/70 dark:group-hover:bg-[#232323]"
                >
                  <img
                    :src="song.cover"
                    alt="Cover"
                    class="w-full aspect-square object-cover rounded-md shadow-sm dark:shadow-[0_8px_24px_rgba(0,0,0,0.5)]"
                  />
                  <div
                    class="absolute bottom-4 right-4 bg-orange-500 rounded-full p-3 opacity-0 group-hover:opacity-100 transition-all translate-y-2 group-hover:translate-y-0 shadow-lg"
                  >
                    <svg class="w-5 h-5 text-white" fill="currentColor" viewBox="0 0 24 24">
                      <path d="M8 5v14l11-7z" />
                    </svg>
                  </div>
                </div>
                <h3 class="font-bold truncate text-base text-gray-900 dark:text-white">
                  {{ song.judul }}
                </h3>
                <p class="text-sm truncate mt-1 text-gray-500 dark:text-gray-400">
                  {{ song.artis }}
                </p>
              </div>
            </div>
          </section>
        </div>

        <div v-else-if="halamanAktif === 'songDetail'" class="w-full max-w-5xl mx-auto mt-4">
          <button
            @click="halamanAktif = 'home'"
            class="mb-6 flex items-center gap-2 text-gray-500 hover:text-orange-500 transition-colors font-bold"
          >
            ← Back to Home
          </button>

          <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
            <div
              class="lg:col-span-5 bg-white dark:bg-[#181818] p-6 rounded-2xl shadow-md border border-gray-100 dark:border-transparent flex flex-col items-center"
            >
              <img
                :src="laguTerpilih?.cover"
                v-on:click="isFullScreen = true"
                alt="Cover Detail"
                class="w-full aspect-square object-cover rounded-lg shadow-xl cursor-pointer hover:scale-[1.02] transition-transform"
              />

              <h1 class="text-2xl font-extrabold mt-6 text-center truncate w-full">
                {{ laguTerpilih?.judul }}
              </h1>
              <p class="text-sm text-gray-500 dark:text-gray-400 mt-1 text-center truncate w-full">
                {{ laguTerpilih?.artis }}
              </p>

              <audio
                ref="audioRef"
                :src="laguTerpilih?.audio"
                @ended="nextLagu"
                @timeupdate="updateWaktuLagu"
                @loadedmetadata="loadDurasiLagu"
              ></audio>

              <div class="w-full mt-6 space-y-1">
                <input
                  type="range"
                  min="0"
                  :max="durasiTotal"
                  step="1"
                  v-model="waktuBerjalan"
                  @input="geserDurasiLagu"
                  class="duration-slider w-full cursor-pointer"
                  :style="{
                    '--track-color': `linear-gradient(to right, #f97316 ${(waktuBerjalan / durasiTotal) * 100}%, #374151 ${(waktuBerjalan / durasiTotal) * 100}%)`,
                  }"
                />
                <div class="flex justify-between text-xs text-gray-400 font-mono">
                  <span>{{ konversiMenitDetik(waktuBerjalan) }}</span>
                  <span>{{ konversiMenitDetik(durasiTotal) }}</span>
                </div>
              </div>

              <div class="flex items-center gap-8 mb-6">
                <button @click="prevLagu" class="text-gray-400 hover:text-orange-500 transition">
                  <svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M6 6h2v12H6zm3.5 6l8.5 6V6z" />
                  </svg>
                </button>

                <button
                  @click="togglePlay"
                  class="w-14 h-14 bg-orange-500 rounded-full flex items-center justify-center text-white hover:bg-orange-600 transition shadow-lg"
                >
                  <svg
                    v-if="!isPlaying"
                    class="w-8 h-8 ml-1"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path d="M8 5v14l11-7z" />
                  </svg>
                  <svg v-else class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z" />
                  </svg>
                </button>

                <button @click="nextLagu" class="text-gray-400 hover:text-orange-500 transition">
                  <svg class="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M6 18l8.5-6L6 6v12zM16 6v12h2V6h-2z" />
                  </svg>
                </button>
              </div>

              <div class="flex items-center gap-4 w-full px-8">
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M15.536 8.464a5 5 0 010 7.072M12 6.75l-4.5 4.5H4.5v3h3l4.5 4.5V6.75z"
                  />
                </svg>
                <input
                  type="range"
                  min="0"
                  max="1"
                  step="0.01"
                  v-model="volumeLevel"
                  @input="aturVolume"
                  class="w-full accent-orange-500 cursor-pointer"
                />
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M19.114 5.636a9 9 0 010 12.728M15.536 8.464a5 5 0 010 7.072"
                  />
                </svg>
              </div>

              <button
                @click="tontonMvLagu"
                class="mt-6 w-full text-center border border-orange-500 text-orange-500 hover:bg-orange-500 hover:text-white px-4 py-2 rounded-full font-bold transition text-xs"
              >
                Watch Music Video
              </button>
            </div>

            <div
              class="lg:col-span-7 bg-white dark:bg-[#181818] p-6 rounded-2xl shadow-md border border-gray-100 dark:border-transparent flex flex-col h-[460px]"
            >
              <div class="flex border-b border-gray-100 dark:border-gray-800 pb-2 mb-4">
                <button
                  @click="tabKananAktif = 'queue'"
                  :class="
                    tabKananAktif === 'queue'
                      ? 'text-orange-500 border-b-2 border-orange-500 font-bold'
                      : 'text-gray-400 font-semibold'
                  "
                  class="px-4 py-2 text-sm transition-all"
                >
                  Next Up (Queue List)
                </button>
                <button
                  @click="tabKananAktif = 'lyrics'"
                  :class="
                    tabKananAktif === 'lyrics'
                      ? 'text-orange-500 border-b-2 border-orange-500 font-bold'
                      : 'text-gray-400 font-semibold'
                  "
                  class="px-4 py-2 text-sm transition-all"
                >
                  Lyrics
                </button>
              </div>

              <div class="flex-1 overflow-y-auto pr-2">
                <div v-if="tabKananAktif === 'queue'" class="space-y-2">
                  <div
                    v-for="song in daftarLagu"
                    :key="song.id"
                    @click="bukaDetailLagu(song)"
                    :class="
                      song.id === laguTerpilih?.id
                        ? 'bg-orange-50 dark:bg-orange-950/20 border-orange-400'
                        : 'hover:bg-gray-50 dark:hover:bg-[#232323] border-transparent'
                    "
                    class="flex items-center gap-4 p-2 rounded-xl cursor-pointer border transition-all"
                  >
                    <span class="text-xs text-gray-400 font-mono w-4 text-center">{{
                      song.id
                    }}</span>
                    <img
                      :src="song.cover"
                      alt="Queue Cover"
                      class="w-10 h-10 object-cover rounded-md"
                    />
                    <div class="flex-1 min-w-0">
                      <p
                        :class="
                          song.id === laguTerpilih?.id ? 'text-orange-500 font-bold' : 'font-medium'
                        "
                        class="text-sm truncate"
                      >
                        {{ song.judul }}
                      </p>
                      <p class="text-xs text-gray-500 dark:text-gray-400 truncate">
                        {{ song.artis }}
                      </p>
                    </div>
                    <span
                      v-if="song.id === laguTerpilih?.id"
                      class="text-xs text-orange-500 font-bold animate-pulse px-2"
                      >Playing</span
                    >
                  </div>
                </div>

                <div
                  v-else-if="tabKananAktif === 'lyrics'"
                  class="text-center font-medium text-gray-600 dark:text-gray-300 space-y-4 py-4 leading-relaxed whitespace-pre-line text-sm"
                >
                  <p class="text-xs text-orange-500 tracking-wider uppercase mb-2">
                    [ Lyrics for: {{ laguTerpilih?.judul }} ]
                  </p>
                  {{ laguTerpilih?.lirik || 'Lirik belum tersedia untuk lagu ini.' }}
                </div>
              </div>
            </div>
          </div>
        </div>

        <div v-else-if="halamanAktif === 'mv'">
          <header class="mb-8 mt-4 flex flex-col gap-1">
            <h1 class="text-4xl font-extrabold tracking-tight">Music Videos</h1>
            <p class="text-xl font-medium text-gray-500 dark:text-gray-400 mt-2">
              Watch stunning visuals of your favorite songs.
            </p>
          </header>

          <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
            <div
              v-for="vid in daftarVideo"
              :key="vid.id"
              @click="bukaDetailVideo(vid)"
              class="bg-white dark:bg-[#181818] rounded-xl overflow-hidden shadow-sm hover:shadow-md cursor-pointer group border border-gray-100 dark:border-transparent transition-all"
            >
              <div class="relative aspect-video overflow-hidden">
                <img :src="vid.thumbnail" class="w-full h-full object-cover" />
                <div
                  class="absolute inset-0 bg-transparent group-hover:bg-black/50 flex items-center justify-center transition-colors duration-200"
                >
                  <div
                    class="hidden group-hover:flex w-14 h-14 bg-orange-500 rounded-full items-center justify-center text-white shadow-lg"
                  >
                    <svg class="w-6 h-6 ml-1" fill="currentColor" viewBox="0 0 24 24">
                      <path d="M8 5v14l11-7z" />
                    </svg>
                  </div>
                </div>
              </div>
              <div class="p-5">
                <h3 class="font-bold text-lg text-gray-900 dark:text-white truncate">
                  {{ vid.judul }}
                </h3>
                <p class="text-sm text-gray-500 dark:text-gray-400 mt-1">{{ vid.artis }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-else-if="halamanAktif === 'mvDetail'" class="w-full max-w-5xl mx-auto mt-4">
          <button
            @click="halamanAktif = 'songDetail'"
            class="mb-6 flex items-center gap-2 text-gray-500 hover:text-orange-500 transition-colors font-bold"
          >
            ← Back to Song Detail
          </button>

          <div
            class="bg-black rounded-2xl overflow-hidden shadow-2xl aspect-video w-full mb-6 border border-gray-800"
          >
            <video
              controls
              class="w-full h-full outline-none"
              :src="videoTerpilih?.videoUrl"
              :poster="videoTerpilih?.thumbnail"
            >
              Browser kamu tidak mendukung pemutar video ini.
            </video>
          </div>

          <div
            class="flex justify-between items-center bg-white dark:bg-[#181818] p-4 rounded-2xl shadow-sm border border-gray-100 dark:border-transparent mb-6"
          >
            <button @click="prevVideo" class="text-orange-500 font-bold hover:underline">
              &laquo; Previous Video
            </button>
            <button @click="nextVideo" class="text-orange-500 font-bold hover:underline">
              Next Video &raquo;
            </button>
          </div>

          <div
            class="bg-white dark:bg-[#181818] p-6 rounded-2xl shadow-sm border border-gray-100 dark:border-transparent"
          >
            <h1 class="text-3xl font-extrabold text-gray-900 dark:text-white">
              {{ videoTerpilih?.judul }}
            </h1>
            <p class="text-lg font-semibold text-orange-500 mt-2">{{ videoTerpilih?.artis }}</p>
            <div class="mt-5 pt-5 border-t border-gray-100 dark:border-gray-800">
              <p class="text-gray-600 dark:text-gray-300 leading-relaxed text-sm">
                {{ videoTerpilih?.deskripsi }}
              </p>
            </div>
          </div>
        </div>

        <div v-else-if="halamanAktif === 'profile'" class="max-w-xl mx-auto mt-4">
          <h1 class="text-4xl font-extrabold mb-8">Edit Profile</h1>

          <div
            class="bg-white dark:bg-[#181818] p-6 rounded-2xl shadow-md border border-gray-100 dark:border-transparent space-y-6"
          >
            <div class="flex flex-col items-center space-y-4">
              <div class="relative group">
                <img
                  :src="
                    username && !fotoProfil
                      ? 'https://ui-avatars.com/api/?name=' +
                        username +
                        '&background=f97316&color=fff'
                      : fotoProfil
                  "
                  alt="Profile Large"
                  class="w-32 h-32 rounded-full object-cover border-4 border-orange-500 shadow-md"
                />
              </div>

              <label
                class="cursor-pointer bg-orange-500 hover:bg-orange-600 text-white text-sm font-semibold px-4 py-2 rounded-lg shadow-sm transition-colors flex items-center gap-2"
              >
                <span v-if="isUploadingProfile">
                  <svg
                    class="animate-spin h-4 w-4 text-white inline"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                  >
                    <circle
                      class="opacity-25"
                      cx="12"
                      cy="12"
                      r="10"
                      stroke="currentColor"
                      stroke-width="4"
                    ></circle>
                    <path
                      class="opacity-75"
                      fill="currentColor"
                      d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
                    ></path>
                  </svg>
                  Uploading...
                </span>
                <span v-else>Upload New Image</span>
                <input
                  type="file"
                  accept="image/*"
                  @change="handleUploadFoto"
                  class="hidden"
                  :disabled="isUploadingProfile"
                />
              </label>
              <p class="text-xs text-gray-400">Max size 1MB</p>
            </div>

            <div class="space-y-2">
              <label class="block text-sm font-semibold text-gray-700 dark:text-gray-300"
                >Username</label
              >
              <input
                type="text"
                v-model="username"
                placeholder="Masukkan username baru..."
                class="w-full p-3 bg-gray-50 dark:bg-[#282828] border border-gray-300 dark:border-transparent rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-500 text-sm"
              />
            </div>

            <div class="space-y-2">
              <label class="block text-sm font-semibold text-gray-700 dark:text-gray-300"
                >Theme Preference</label
              >
              <div class="flex gap-6 pt-1">
                <label class="flex items-center gap-2 cursor-pointer text-sm">
                  <input
                    type="radio"
                    :value="false"
                    v-model="isDarkMode"
                    class="accent-orange-500 w-4 h-4"
                  />
                  Light Mode
                </label>
                <label class="flex items-center gap-2 cursor-pointer text-sm">
                  <input
                    type="radio"
                    :value="true"
                    v-model="isDarkMode"
                    class="accent-orange-500 w-4 h-4"
                  />
                  Dark Mode
                </label>
              </div>
            </div>

            <button
              @click="simpanKeLocalStorage"
              class="w-full bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 rounded-lg shadow-md transition-colors text-sm"
            >
              Save Changes
            </button>
          </div>
        </div>
      </main>

      <div
        v-if="isFullScreen"
        class="fixed inset-0 z-50 bg-black/95 flex flex-col items-center justify-center"
      >
        <div class="absolute top-6 right-6 flex gap-4">
          <button
            @click="zoomIn"
            class="bg-gray-800 text-white w-10 h-10 rounded-full font-bold text-xl hover:bg-gray-700 transition"
          >
            +
          </button>
          <button
            @click="zoomOut"
            class="bg-gray-800 text-white w-10 h-10 rounded-full font-bold text-xl hover:bg-gray-700 transition"
          >
            -
          </button>
          <button
            @click="tutupFullScreen"
            class="bg-red-500 text-white w-10 h-10 rounded-full font-bold hover:bg-red-600 transition"
          >
            X
          </button>
        </div>
        <div class="overflow-hidden w-full h-full flex items-center justify-center mt-12">
          <img
            :src="laguTerpilih?.cover"
            alt="Fullscreen Cover"
            class="transition-transform duration-200"
            :style="`transform: scale(${zoomLevel})`"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// nextTick di-import untuk nunggu elemen HTML selesai di-render sebelum dieksekusi
import { ref, onMounted, watch, nextTick } from 'vue'
import { parse } from 'vue/compiler-sfc'

// ================= STATE PERPINDAHAN HALAMAN =================
const halamanAktif = ref('home')
const daftarLagu = ref([])

// ================= STATE DATA PROFIL USER =================
const username = ref('Guest')
const fotoProfil = ref('')
const isUploadingProfile = ref(false)
const isDarkMode = ref(true)

// ================= STATE SONG DETAIL & PLAYER AUDIO =================
const laguTerpilih = ref(null)
const audioRef = ref(null)
const isPlaying = ref(false)
const volumeLevel = ref(0.5)

// BARU: State pelacakan durasi lagu (dalam satuan detik)
const waktuBerjalan = ref(0)
const durasiTotal = ref(0)

// BARU: State switcher untuk panel sebelah kanan ('queue' atau 'lyrics')
const tabKananAktif = ref('queue')

// ================= STATE FULLSCREEN ZOOM IMAGE =================
const isFullScreen = ref(false)
const zoomLevel = ref(1)

// Watcher untuk sinkronisasi class Dark Mode ke HTML tag
watch(isDarkMode, (modeGelap) => {
  if (modeGelap) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
})

onMounted(() => {
  // Ambil profil dari penyimpanan Local Storage
  const savedUsername = localStorage.getItem('spojedy_username')
  const savedTheme = localStorage.getItem('spojedy_theme')
  const savedFotoBase64 = localStorage.getItem('spojedy_foto_base64')

  if (savedUsername) username.value = savedUsername

  if (savedTheme) {
    isDarkMode.value = savedTheme === 'true'
  }
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }

  if (savedFotoBase64) fotoProfil.value = savedFotoBase64

  const dataLagu = [
    {
      judul: '12 Seconds',
      artis: 'JKT48',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/_MV_%2012%20Seconds%20-%20JKT48%20Team%20Love.mp3?updatedAt=1779543075261',
      lirik: `Permata terindah dari seluruh semesta
Kan kuberikan untukmu
Bisakah sebentar pejamkan kedua matamu?
Kau ucapkan dengan sangat jahil

Terdengar suara laut menghempas pemecah ombak
Dirimu makin mendekat, ’ku merasakannya
(Cinta musim panas) sekarang bermula

Bibir ini pun bersentuhan
Sangat lembut bagai sebuah berlian
Hal berharga yang s'lama ini selalu kau jaga Apa yang harus kulakukan?
Yang kuinginkan hanya satu hal saja Menerimamu dalam dekapanku Diriku terpaku twelve seconds
Saatnya cukup kah? Kuintip sedikit saja
Kita pun saling memandang
 
B'rapa rata-rata lamanya yang dibutuhkan
*Di saat saling berciuman?*


Oh, terlalu romantis, apa yang terjadi set’lah ini? Wajah dan juga apakah yang 'kan kukatakan? (Tak mungkin kеmbali) s'batas teman lagi

Bibir yang saling berjauhan Bagai kehilangan sеbuah berlian
Mulai hari ini 'kan kukenang sampai s'lamanya Bisakah s'perti ini saja
Dengan air laut yang membelai hangat Biarkanku seorang milikimu
Rather than forever, twelve seconds 
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/JKT48%20-%2012%20Seconds.png?updatedAt=1779543100336',
    },
    {
      judul: 'On Bended Knee',
      artis: 'Boyz II Men',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Boyz%20II%20Men%20-%20On%20Bended%20Knee.mp3?updatedAt=1779543074941',
      lirik: `Darlin' I, I can't explain
Where did we lose our way Girl it's drivin' me insane
And I know I just need one more chance To prove my love to you
And if you come back to me I'll guarantee
That I'll never let you go

Can we go back to the days our love was strong? Can you tell me how a perfect love goes wrong? Can somebody tell me how to get things back The way they use to be?
Oh God give me a reason I'm down on bended knee
I'll never walk again until you come back to me I'm down on bended knee

 
So many nights I dream of you Holding my pillow tight
And I know I don't need to be alone
When I open up my eyes To face reality
Every moment without you It seems like eternity
I'm begging you, begging you come back to me

Can we go back to the days our love was strong? Can you tell me how a perfect love goes wrong? Can somebody tell me how to get things back The way they use to be?
Oh God give me a reason I'm down on bended knee
I'll never walk again until you come back to me I'm down on bended knee

Baby, I'm sorry
Please forgive me for all the wrong I've done Please come back home, girl
I know you put all your trust in me I'm sorry I let you down
Please forgive me

I'm gonna swallow my pride, say I'm sorry
 
Stop pointing fingers, the blame is on me I want a new life, and I want it with you
If you feel the same, don't ever let it go You gotta believe in the spirit of love It'll heal all things, it won't hurt anymore No, I don't believe our love's terminal

Come home


Can we go back to the days our love was strong? Can you tell me how a perfect love goes wrong? Can somebody tell me how to get things back The way they used to be?
Oh God give me a reason I'm down on bended...
Down on bended knee
I'll never walk again until you come back to me I'm down on bended knee
Can we go back to the days our love was strong Can you tell me how a perfect love goes wrong Can somebody tell me how to get things back The way they use to be
Oh God give me a reason I'm down on
Down on bended knee
I'll never walk again until you come back to me
 
I'm down on bended knee


I'll never walk again
Until you come back to me I'm down on bended knee
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Boyz%20II%20Men%20-%20On%20Bended%20Knee.png?updatedAt=1779543099501',
    },
    {
      judul: 'Orang ke 3',
      artis: 'HIVI!',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/HIVI!%20-%20Orang%20ke%203%20(Official%20Music%20Video).mp3?updatedAt=1779543074713',
      lirik: `Saat berjumpa dan kau menyapa Indah parasmu hangatkan suasana
Buatku tak percaya, mimpi indahku jadi nyata Saat sendiri jalani hari
Bayang-bayangmu selalu menghampiri Dan aku pun mengerti apa maunya hati ini
Namun tiba-tiba kau ada yang punya Hati ini terluka
Sungguh ku kecewa Ingin ku berkata
Kasih maaf bila aku jatuh cinta Maaf bila saja ku suka
Saat kau ada yang punya Haruskah kupendam rasa ini saja Ataukah kuteruskan saja
 
Hingga kau meninggalkannya dan kita bersama

Namun tiba tiba kau ada yang punya Hati ini terluka (Terluka)
Sungguh ku kecewa (Sungguh ku kecewa)
Ingin ku berkata

Kasih maaf bila aku jatuh cinta Maaf bila saja ku suka
Saat kau ada yang punya Haruskah kupendam rasa ini saja Ataukah kuteruskan saja
Hingga kau meninggalkannya dan kita bersama

Akankah ada kesempatan Untuk diriku menyatakan Rasa yang selama ini ada

Kasih maaf bila aku jatuh cinta (Maaf bila kau jatuh cinta) Maaf bila saja ku suka (Maaf saja bila kau suka)
Saat kau ada yang punya Haruskah kupendam rasa ini saja Ataukah kuteruskan saja
Hingga kau meninggalkannya dan kita bersama Kasih maaf bila aku jatuh cinta
 
Maaf bila saja ku suka Saat kau ada yang punya
Haruskah kupendam rasa ini saja Ataukah kuteruskan saja
Hingga kau meninggalkannya dan kita bersama
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Hivi%20-%20Orang%20ke%203.jpg?updatedAt=1779543099819',
    },
    {
      judul: 'Shape Of My Heart',
      artis: 'Bacstreet Boys',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Backstreet%20Boys%20-%20Shape%20Of%20My%20Heart%20(Official%20HD%20Video).mp3?updatedAt=1779543074232',
      lirik: `Hmm, mmmh, yeah, yeah

Baby, please try to forgive me Stay here, don't put out the glow Hold me now don't bother
If every minute it makes me weaker You can save me from the man That I've become, oh yeah

Looking back on the things I've done I was trying to be someone
I played my part, kept you in the dark
Now let me show you the shape of my heart

Sadness is beautiful
Loneliness is trying to call you
 
So help me I can't wait there's more, oh no
Touch me now, don't bother
If I was thinkin' it makes me weaker
You can save me from the man I've become

Looking back on the things I've done I was trying to be someone
I played my part, kept you in the dark (In the dark)
Now let me show you the shape of my heart


I'm here with my confession Got nothing to hide no more I don't know where to start
But to show you the shape of my heart

I'm lookin' back on things I've done
I never wanna play the same old part
I'll keep you in the dark (Keep you in the dark)
Now let me show you the shape of my heart (Heart!)

Looking back on the things I've done
I was trying to be someone (Trying to be someone)
I played my part, kept you in the dark
Now let me show you the shape of my heart
(Now let me show you the true shape of my heart!)
Looking back on the things I've done I was trying to be someone
I played my part, kept you in the dark Now let me show you the shape of
 

Show you the shape of my heart
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Backstreet%20Boys%20-%20Shape%20Of%20My%20Heart.png?updatedAt=1779543099037',
    },
    {
      judul: 'Raja Hati',
      artis: 'JKT48',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Raja%20Hati%20-%20JKT48%20Special%20Performance%20Video.mp3?updatedAt=1779543074241',
      lirik: `Bila cinta permainan
Kau ‘kan coba kudapatkan Kupertaruhkan semua 'tuk masa depan Karena bagi hatiku kaulah harapan

Bagai dadu berputar ‘ku ke sana kemari
Wahai kau Raja Hati, di manakah kau sembunyi?

Jantungku berontak, mata kita beradu Kaulah kartu terindah yang ada di hidupku Mari menyusun kisah
Mimpiku dan mimpimu Tak ingin berpisah
‘Kan kujaga kau s’lamanya di hidupku
 
Meski tahu kau menahan ‘Ku yakin kau merasakan
Kupertaruhkan semua 'tuk masa depan Kar'na hati ini berkata engkaulah harapan

Bagai dadu berputar ‘ku ke sana kemari
Mana kau Raja Hati? Berhentilah kau sembunyi


Jantungku berontak, mata kita beradu Kaulah kartu terindah yang ada di hidupku Mari menyusun kisah
Mimpiku dan mimpimu Tak ingin berpisah
‘Kan kujaga kau s’lamanya di hidupku

Sha-la-la, la-la-la, la-la-la La-la-la-la, la-la-la
La-la-la-la, la-la-la, haa

Jantungku berontak, mata kita beradu Jantungku berontak, mata kita beradu Kaulah kartu terindah yang ada di hidupku Mari menyusun kisah
Mimpiku dan mimpimu
 
Tak ingin berpisah
‘Kan kujaga kau s’lamanya di hidupku

Jantungku berontak, mata kita beradu Kaulah kartu terindah yang ada di hidupku Mari menyusun kisah
Mimpiku dan mimpimu Tak ingin berpisah
‘Kan kujaga kau s’lamanya di hidupku
Oh, ‘kan kujaga kau s’lamanya di hidupku ‘Kan kujaga kau s’lamanya di hidupku
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/JKT48%20-%20Raja%20Hati.png?updatedAt=1779543100195',
    },
    {
      judul: 'Hujan',
      artis: 'Utopia',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Utopia%20-%20Hujan%20%20Official%204K%20Remastered%20Video.mp3?updatedAt=1779543074026',
      lirik: `Rinai hujan basahi aku temani sepi yang mengendap Kala aku mengingatmu dan semua saat manis itu
 
Segalanya seperti mimpi, kujalani hidup sendiri Andai waktu berganti, aku tetap tak 'kan berubah

Aku selalu bahagia saat hujan turun
Kar'na aku dapat mengenangmu untukku sendiri, o-o-oh

Selalu ada cerita tersimpan di hatiku
Tentang kau dan hujan, tentang cinta kita yang mengalir seperti air

Aku selalu bahagia saat hujan turun
Kar'na aku dapat mengenangmu untukku sendiri, o-o-oh

Aku bisa tersenyum (La-la-la-la-la) Sepanjang hari
Kar'na hujan pernah Menahanmu di sini untukku

Aku selalu bahagia saat hujan turun
Kar'na aku dapat mengenangmu untukku sendiri, o-o-oh
Aku bisa tersenyum sepanjang hari
Kar'na hujan pernah menahanmu di sini untukku
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Utopia%20-%20Hujan.jpg?updatedAt=1779543099878',
    },
    {
      judul: 'Mo Koi Nante Shinai',
      artis: 'Noriyuki Makihara',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/_%E5%85%AC%E5%BC%8F_%E6%A7%87%E5%8E%9F%E6%95%AC%E4%B9%8B_%E3%82%82%E3%81%86%E6%81%8B%E3%81%AA%E3%82%93%E3%81%A6%E3%81%97%E3%81%AA%E3%81%84_(MV)_5th%E3%82%B7%E3%83%B3%E3%82%B0%E3%83%AB_%20(1992%E5%B9%B4)%20Noriyuki%20MakiharaMo%20Koinante%20Shinai%20(1).mp3?updatedAt=1779543073744',
      lirik: `Kimi ga inai to nan ni mo Dekinai wake ja nai to Yakan o hi ni kaketa kedo
Koucha no arika ga wakaranai
Hora choushoku mo tsukureta mon ne Dakedo amari oishikunai
Kimi ga tsukutta no nara monku mo Omoikiri ieta noni

Issho ni iru toki wa Kyuukutsu ni omoeru kedo Yatto jiyuu o te ni ireta
Boku wa motto sabishiku natta

Sayonara to itta kimi no Kimochi wa wakaranai kedo Itsumo yori nagame ga ii
Hidari ni sukoshi tomadotteru yo Moshi kimi ni hitotsu dake Tsuyogari o ieru no nara
Mou koi nante shinai nante Iwanai yo zettai
 
Nihon naranda haburashi mo Ippon sutete shimaou
Kimi no shumi de katta fuku mo Mottainai kedo sutete shimaou "otokorashiku isagiyoku" to Gomibako kakaeru boku wa
Hoka no dare kara mite mo ichiban Senchimentaru daro
Konna ni ippai no
Kimi no nukegara atsumete Muda na mono ni kakomarete Kurasu no mo shiawase to shitta

Kimi ate no yuubin ga Posuto ni todoiteru uchi wa
Katasumi de mayotte iru
Senaka o omottе shinpai da kedo Futari de dasenakatta
Kotaе wa kondo aeraeru Kimi no shiranai dareka to Mitsukete miseru kara

Hontou ni hontou ni
Kimi ga daisuki datta kara Mou koi nante shinai nante Iwanai yo zettai
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/%E6%A7%87%E5%8E%9F%E6%95%AC%E4%B9%8B%20(Noriyuki%20Makihara)%20-%20%E3%82%82%E3%81%86%E6%81%8B%E3%81%AA%E3%82%93%E3%81%A6%E3%81%97%E3%81%AA%E3%81%84%20(Mou%20Koinante%20Shinai).jpg?updatedAt=1779543099892',
    },
    {
      judul: 'Ruang Baru',
      artis: 'Barsena Bestandhi',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Official%20Music%20Video%20Ruang%20Baru%20(Feat.%20Angga%20Yunanda)%20%20OST.%20My%20Annoying%20Brother%20(Final%20Trailer).mp3?updatedAt=1779543073617',
      lirik: `Bagaikan kemarau yang panjang Kurindukan turunnya hujan

Waktu yang berselang, menunggumu pulang Kembali mengulang kenangan
Masa-masa indah, senyum bahagia Yang mungkin takkan lagi datang
Bagaikan sungai yang bercabang Bertemu di laut yang sama

Begitupun juga kita manusia Ada pisah dan pertemuan
Tangisan dan tawa, sedih dan bahagia Tak kekal hanya sementara

 
Usap pelan air mataku Sadari waktu akan berlalu Rindu yang lalu 'kan jadi satu Senyumlah bersamaku Sabarlah menunggu
Kita 'kan bertemu di ruang baru


[Instrumental Break]

Usap pelan air mataku Sadari waktu akan berlalu Rindu yang lalu 'kan jadi satu Senyumlah bersamaku Sabarlah menunggu
Kita 'kan bertemu di ruang baru

Kita 'kan bertemu di ruang baru
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Barsena%20Bestandhi%20-%20Ruang%20Baru.jpg?updatedAt=1779543098944',
    },
    {
      judul: 'What is Love',
      artis: 'TWICE',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/TWICE%20What%20is%20Love%20MV.mp3?updatedAt=1779543072370',
      lirik: `TWICE!
What is love?

Maeilgachi yeonghwa sogeseona Chaek sogeseona
Deurama sogeseo sarangeul neukkyeo Mm, sarangeul baewo
Nae ilcheoreom jakku gaseumi ttwieo Dugeundugeungeoryeo
Seolleime bupureo olla
 
Mm, gunggeumhaeseo michil geonman gata

Ooh, eonjengan naegedo
Ireon iri siljero ireonalkka? (Ooh)
Geuge eonjejjeumilkka? Eotteon saramilkka?

(I wanna know) Satangcheoreom dalkomhadaneunde (I wanna know) Haneureul naneun geot gatdaneunde (I wanna know, know, know, know, what is love?)
Sarangi eotteon neukkiminji
(I wanna know) Haru jongil utgo itdaneunde
(I wanna know) Sesangi da areumdapdaneunde
(I wanna know, know, know, know, what is love?)
Eonjengan naegedo sarangi olkka?

Jigeum ireon sangsangmaneurodo Tteoollyeoman bwado
Gaseumi teojil geot gateunde Mm, ireoke joeunde
Manil eonjenga jinjjaro naege Sarangi ol ttae
Nan ureobeoriljido molla
Mm, jeongmal gunggeumhae, michil geonman gata 
 
Ooh, eonjengan naegedo
Ireon iri siljero ireonalkka? (Ooh)
Geuge eonjejjeumilkka?
Eotteon saramilkka?

(I wanna know) Satangcheoreom dalkomhadaneunde (I wanna know) Haneureul naneun geot gatdaneunde (I wanna know, know, know, know, what is love?)
Sarangi eotteon neukkiminji
(I wanna know) Haru jongil utgo itdaneunde
(I wanna know) Sesangi da areumdapdaneunde
(I wanna know, know, know, know, what is love?)
Eonjengan naegedo sarangi olkka?


Jigeum sesang eoneu gose salgo inneunji Dodaeche eonjejjeum nawa mannage doelleunji Eonje eotteoke uriui inyeoneun
Sijakdoelleunji moreujiman neukkimi eojjeonji
Jinjja joeul geot gata waenji
Yeonghwa deuramabodado deo meotjin (Meotjin) Sarangi ol geoya, nae yegam eonjena matji (Ooh-ooh) Eoseo natanabwa, naneun da junbiga dwaetji, ready

 (Eodi isseulkka?) Chajanael geoya
(Eodi isseulkka?) Bogo sipeo jukgesseo Deo isang chameul su
 
Eopseul geonman gata

Satangcheoreom dalkomhadaneunde Haneureul naneun geot gatdaneunde
(I wanna know, know, know, know, what is love?) Sarangi eotteon neukkiminji
Haru jongil utgo itdaneunde Sesangi da areumdapdaneunde
(I wanna know, know, know, know, what is love?)
Eonjengan naegedo sarangi olkka?


I wanna know (Ooh, what is love?) I wanna know (I wanna know)
I wanna know, know, know, know, what is love?
I wanna know, I wanna know, what is love?
I wanna know I wanna know
I wanna know, know, know, know, what is love? I wanna know
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Twice%20-%20What%20is%20Love.jpg?updatedAt=1779543099926',
    },
    {
      judul: 'Bling Bang Bang Born',
      artis: 'Creepy Nuts',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Bling-Bang-Bang-Born%20(Official%20Music%20Video).mp3?updatedAt=1779543071549',
      lirik: `Yeah, boy

 
Chiito, gifted, arawaza, wanted Kinki, kinjite, akiraka mouten
Hansoku, ijigen, kono yo no mon de wa nai desu Muri gee, sore kiitenai tte
Ay, raibaru kuchi wo soroete Wow, raibaru kuchi wo soroete
Bagu de, magure, mitomenee zettee Maji de? Kore wo ma
Zenbu namami de?


It's namami, it's namami, yeah-yeah-yeah-yeah Bling-bang-bang, bling-bang-bang-born
Bling-bang-bang, bling-bang-bang-born

Jitsuryoku wo hakki shikiru mae ni Aite no hou ga bakkurete kurashii Agarikiru haadoru very happy Akiraka ni dantotsu de pikaichi
Aika warazu dappi shiteru mainichi (Bling, bling, bling) Dare no nanahikari mo iranai omae no ice yori icy (Icy) Ore, patto mi dekinai koto bakkari da kedo very happy Aa, kiretеru, akireteru mawari
Megu marеteru kazoku tomodachi (Happy)
Mou hansoku teki tachiichi, mina ore ni makase tokeba ii (Bang-bang-bang)
Kyoukasho ni nai, mondaishuu ni nai Chou bad na majinai, listen
 

Kagami yo kagami kotaechatte
Who's the best? I'm the best! Oh yeah Namami no mama ikeru toko made To the next, to the ichiban ue

Now singin'
Bling-bang-bang, bling-bang-bang, bling-bang-bang-born (Now singin')
Bling-bang-bang, bling-bang-bang, bling-bang-bang-born (Now singin')
Bling-bang-bang, bling-bang-bang, bling-bang-bang-born To the next, to the ichiban ue


Ey-day, ore no mama de iru dake de chou flex Ey-day, daremo kuchi wo hasamenai (Don't test) Ey-day, ore no mama de iru dake de chou flex
Ey-day, daremo kuchi wo hasamasenai (Don't test)

Yeah, yeah, yeah
Gakureki mo nai zenka mo nai yoyuu de bling-bling
Kono sonzai jitai ga bunkazai na noumiso bling-bling Koukyuusha wa kaeru menkyo wa nai aisha green, green Zenkoku kakuchi yurasu ippin
Kono bero ga bling-bling
 
Baretto nara mantan
Kansai namari namami no kotodama
Ongaku, kouun, shouri no megami, koyoi mo sanmata bang-bang Manga mitai na yakara to manma de hariaete shimatteru manga Attou teki chikara kono atama to kuchi kara
Kono karada tattoo wa haittenai Kono tsura ni kizu mo tsuitenai Kurikaeshi yarakashiteku dameeji ga Ikatsui nenrin wo kizamu shiwa
Bling-bang-bang, bling-bang-bang, bling-bang-bang-born Ore no mama de bling shite, bang shite, bang suru tame ni Born shite kita nippon, ay!
Kagami yo kagami kotaechatte
Who's the best? I'm the best! Oh yeah Namami no mama ikeru toko made To the next, to the ichiban ue
Now singin' bling-bang-bang, bling-bang-bang, bling-bang-bang-born (Now singin') Bling-bang-bang, bling-bang-bang, bling-bang-bang-born (Now singin') Bling-bang-bang, bling-bang-bang, bling-bang-bang-born To the next, to the ichiban ue
Ey-day, ore no mama de iru dake de chou flex Ey-day, daremo kuchi wo hasamenai (Don't test)
 
Ey-day, ore no mama de iru dake de chou flex
Ey-day, daremo kuchi wo hasamasenai (Don't test)
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Bling-Bang-Bang-Born.png?updatedAt=1779543099645',
    },
    {
      judul: 'Wind',
      artis: 'Akeboshi',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Akeboshi_Wind_OFFICIAL%20MUSIC%20VIDEO.mp3?updatedAt=1779543070738',
      lirik: `Cultivate your hunger before you idealize Motivate your anger to make them all realize Climbing the mountain, never coming down Break into the contents, never falling down

My knee is still shaking like I was twelve Sneaking out the classroom by the back door
A man railed at me twice, though, but I didn't care Waiting is wasting for people like me

Don't try to live so wise Don't cry 'cause it's alright Don't try with fakes or fears
'Cause you will hate yourself in the end Don't try to live so wise
Don't cry 'cause it's alright Don't try with fakes or fears
'Cause you will hate yourself in the end

You say "Dreams, are dreams"
 
I ain't gonna play the fool, anymore You say "'Cause I've still got my soul!"

Take your time, baby, your blood needs slowing down Breach yourself to reach yourself before you gloom Reflection of fear makes shadows of nothing Shadows of nothing (Shadow of nothing)

You still are blind if you see a winding road
'Cause there's always a straight way to the point you seek

Don't try to live so wise Don't cry 'cause it's alright Don't try with fakes or fears
'Cause you will hate yourself in the end Don't try to live so wise
Don't cry 'cause it's alright Don't try with fakes or fears
'Cause you will hate yourself in the end Don't try to live so wise
Don't cry 'cause it's alright Don't try with fakes or fears
'Cause you will hate yourself in the end
'Cause you will hate yourself in the end
 
'Cause you will hate yourself in the end 'Cause you will hate yourself in the end 'Cause you will hate yourself in the end
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Akeboshi%20-%20Wind.png?updatedAt=1779543100204',
    },
    {
      judul: 'Follow the Light',
      artis: 'Chen Zhuoxuan',
      audio:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Audio/Chen%20Zhuoxuan%20%E7%A1%AC%E7%B3%96%E5%B0%91%E5%A5%B3303%E9%99%88%E5%8D%93%E7%92%87-Follow%20the%20Light%20%E8%BF%BD%E9%9A%8F%E5%85%89%20%20Official%20MV%20(Falling%20Into%20Your%20Smile%20OST_%E4%BD%A0%E5%BE%AE%E7%AC%91%E6%97%B6%E5%BE%88%E7%BE%8E_%E4%B8%BB%E9%A2%98%E6%9B%B2).mp3?updatedAt=1779543068536',
      lirik: `誰的道理和期待 似乎並不是我內心獨白做自己還是逃開 難道就這樣隨風搖擺 燦爛星海 是你 走過來
那些角落 意外 的打開
看來我的 無奈 有人真的 會明白

漸漸離開的孤單 開始相信 默契的存在命運能夠被改變 因為堅持 就不曾蒼白指尖之下多少 的成敗
明日之上歡呼 的人海
你的目光讓我更 熱愛 oh yeah
 
如果懷揣著 一個夢 我想要追隨光就算有無數的跌倒 路再難也一樣身披荊棘腳踏 的熾沙
劇情反轉時光 的懸崖
至少當我們都知道那是要去的 遠方

如果懷揣著 一個夢 我就要追隨光
原來 我們在 熱望刹那 終會把黑夜燃亮無人能解的倔強多傻
重返榮耀的心就多大
記得 那一刻 巔峰上 一起迎接陽光一起迎接陽光

你是否 還記得陪你看流星劃過多少回 像聽到那晚把願望許下我們都 約定好
青春就是不把遺憾留下


如果 懷揣著 一個夢 我就要追隨光我就要追隨光
如果 懷揣著 一個夢 我就要追隨光
原來 我們在 熱望刹那 終會把黑夜燃亮無人能解的倔強多傻
 
重返榮耀的心就多大
記得 那一刻 巔峰上 一起迎接陽光
`,
      cover:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Chen%20Zhuoxuan%20%E7%A1%AC%E7%B3%96%E5%B0%91%E5%A5%B3303%E9%99%88%E5%8D%93%E7%92%87-Follow%20the%20Light%20%E8%BF%BD%E9%9A%8F%E5%85%89%20%20(Falling%20Into%20Your%20Smile%20OST_%E4%BD%A0%E5%BE%AE%E7%AC%91%E6%97%B6%E5%BE%88%E7%BE%8E_%E4%B8%BB%E9%A2%98%E6%9B%B2).png?updatedAt=1779543099575',
    },
  ]

  // Mengisi daftar lagu menggunakan perulangan 'for' konvensional
  dataLagu.forEach((lagu, index) => {
    daftarLagu.value.push({
      id: index + 1,
      judul: lagu.judul,
      artis: lagu.artis,
      cover: lagu.cover,
      audio: lagu.audio,
      lirik: lagu.lirik,
    })
  })

  // Data dummy Music Video (Nanti URL ini diganti dengan CDN ImageKit/Cloudinary milikmu)
  const dataVideoNyata = [
    {
      id: 1,
      judul: '12 Seconds',
      artis: 'JKT48',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/JKT48%20-%2012%20Seconds.png?updatedAt=1779543100336', // GANTI CDN DISINI (Format .jpg/.png rasio 16:9)
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/_MV_%2012%20Seconds%20-%20JKT48%20Team%20Love.mp4', // GANTI CDN DISINI (Format .mp4)
      deskripsi:
        'Video klip resmi yang penuh energi dan keceriaan. Menampilkan koreografi sinkron yang memukau dan visual yang cerah, sangat cocok untuk membangkitkan semangat harimu.',
    },
    {
      id: 2,
      judul: 'On Bended Knee',
      artis: 'Boyz II Men',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Boyz%20II%20Men%20-%20On%20Bended%20Knee.png?updatedAt=1779543099501', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Boyz%20II%20Men%20-%20On%20Bended%20Knee.mp4', // GANTI CDN DISINI
      deskripsi:
        'Klasik R&B era 90-an yang tak lekang oleh waktu. Video bernuansa melankolis ini menampilkan harmoni vokal yang sempurna dan emosi mendalam dari setiap personelnya.',
    },
    {
      id: 3,
      judul: 'Orang ke 3',
      artis: 'HIVI!',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Hivi%20-%20Orang%20ke%203.jpg?updatedAt=1779543099819', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/HIVI!%20-%20Orang%20ke%203%20(Official%20Music%20Video).mp4', // GANTI CDN DISINI
      deskripsi:
        'Visual penuh warna dengan alur cerita ringan khas remaja. Menggambarkan dilema cinta dengan sentuhan musik pop ceria dan melodi gitar akustik yang bikin earworm.',
    },
    {
      id: 4,
      judul: 'Shape of My Heart',
      artis: 'Backstreet Boys',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Backstreet%20Boys%20-%20Shape%20Of%20My%20Heart.png?updatedAt=1779543099037', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Backstreet%20Boys%20-%20Shape%20Of%20My%20Heart%20(Official%20HD%20Video).mp4', // GANTI CDN DISINI
      deskripsi:
        'Penampilan ikonik dari boyband legendaris. Menampilkan set teatrikal dan harmoni vokal yang emosional, membawa kembali nostalgia masa keemasan musik pop 2000-an.',
    },
    {
      id: 5,
      judul: 'Raja Hati',
      artis: 'JKT48',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/JKT48%20-%20Raja%20Hati.png?updatedAt=1779543100195', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Raja%20Hati%20-%20JKT48%20Special%20Performance%20Video.mp4', // GANTI CDN DISINI
      deskripsi:
        'Penampilan panggung live dengan balutan kostum elegan. Menyoroti pesona dan sinkronisasi para member dalam membawakan melodi yang indah dan lirik yang menyentuh.',
    },
    {
      id: 6,
      judul: 'Hujan',
      artis: 'Utopia',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Utopia%20-%20Hujan.jpg?updatedAt=1779543099878', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Utopia%20-%20Hujan%20%20Official%204K%20Remastered%20Video.mp4', // GANTI CDN DISINI
      deskripsi:
        'Video klip bernuansa sedikit kelam dan misterius yang sangat pas dengan genre pop-rock alternatif. Memberikan vibes melankolis yang cocok ditonton saat cuaca sedang mendung.',
    },
    {
      id: 7,
      judul: 'Mo Koi Nante Shinai',
      artis: 'Noriyuki Makihara',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/%E6%A7%87%E5%8E%9F%E6%95%AC%E4%B9%8B%20(Noriyuki%20Makihara)%20-%20%E3%82%82%E3%81%86%E6%81%8B%E3%81%AA%E3%82%93%E3%81%A6%E3%81%97%E3%81%AA%E3%81%84%20(Mou%20Koinante%20Shinai).jpg?updatedAt=1779543099892', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/_%E5%85%AC%E5%BC%8F_%E6%A7%87%E5%8E%9F%E6%95%AC%E4%B9%8B_%E3%82%82%E3%81%86%E6%81%8B%E3%81%AA%E3%82%93%E3%81%A6%E3%81%97%E3%81%AA%E3%81%84_(MV)_5th%E3%82%B7%E3%83%B3%E3%82%B0%E3%83%AB_%20(1992%E5%B9%B4)%20Noriyuki%20MakiharaMo%20Koinante%20Shinai.mp4', // GANTI CDN DISINI
      deskripsi:
        'Video musik retro dari era 90-an Jepang. Menampilkan adegan kehidupan sehari-hari dengan sinematografi klasik yang hangat, menenangkan, dan penuh nostalgia.',
    },
    {
      id: 8,
      judul: 'Ruang Baru',
      artis: 'Barsena Bestandhi',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Barsena%20Bestandhi%20-%20Ruang%20Baru.jpg?updatedAt=1779543098944', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Official%20Music%20Video%20Ruang%20Baru%20(Feat.%20Angga%20Yunanda)%20%20OST.%20My%20Annoying%20Brother%20(Final%20Trailer)%20-%20BASE%20Entertainment%20Indonesia%20(720p,%20h264).mp4', // GANTI CDN DISINI
      deskripsi:
        'Visual estetis dengan color grading yang lembut. Mengisahkan perjalanan emosional menemukan lembaran baru dalam hidup dengan iringan kualitas vokal yang luar biasa.',
    },
    {
      id: 9,
      judul: 'What is Love',
      artis: 'TWICE',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Twice%20-%20What%20is%20Love.jpg?updatedAt=1779543099926', // GANTI CDN DISINI
      videoUrl: 'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/TWICE%20What%20is%20Love%20MV.mp4', // GANTI CDN DISINI
      deskripsi:
        'Video klip super ceria dan penuh warna! Menampilkan parodi kreatif dari berbagai adegan film ikonik dunia dengan koreografi yang sangat catchy dan menyenangkan.',
    },
    {
      id: 10,
      judul: 'Bling Bang Bang Born',
      artis: 'Creepy Nuts',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Bling-Bang-Bang-Born.png?updatedAt=1779543099645', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Bling-Bang-Bang-Born%20(Official%20Music%20Video).mp4', // GANTI CDN DISINI
      deskripsi:
        'Visual dinamis dan super energik! Menampilkan transisi cepat, efek visual mencolok, dan beat hip-hop asyik yang bikin kepala otomatis mengangguk mengikuti irama.',
    },
    {
      id: 11,
      judul: 'Wind',
      artis: 'Akeboshi',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Akeboshi%20-%20Wind.png?updatedAt=1779543100204', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Akeboshi_Wind_OFFICIAL%20MUSIC%20VIDEO.mp4', // GANTI CDN DISINI
      deskripsi:
        'Visual animasi dan sinematografi yang menenangkan, sangat familiar bagi para penggemar anime klasik. Menggabungkan melodi folk indie dengan suasana yang damai.',
    },
    {
      id: 12,
      judul: 'Follow the Light',
      artis: 'Chen Zhuoxuan',
      thumbnail:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/Cover/Chen%20Zhuoxuan%20%E7%A1%AC%E7%B3%96%E5%B0%91%E5%A5%B3303%E9%99%88%E5%8D%93%E7%92%87-Follow%20the%20Light%20%E8%BF%BD%E9%9A%8F%E5%85%89%20%20(Falling%20Into%20Your%20Smile%20OST_%E4%BD%A0%E5%BE%AE%E7%AC%91%E6%97%B6%E5%BE%88%E7%BE%8E_%E4%B8%BB%E9%A2%98%E6%9B%B2).png?updatedAt=1779543099575', // GANTI CDN DISINI
      videoUrl:
        'https://ik.imagekit.io/urywxlbpt/SpoJeDy/MV/Chen%20Zhuoxuan%20%E7%A1%AC%E7%B3%96%E5%B0%91%E5%A5%B3303%E9%99%88%E5%8D%93%E7%92%87-Follow%20the%20Light%20%E8%BF%BD%E9%9A%8F%E5%85%89%20%20Official%20MV%20(Falling%20Into%20Your%20Smile%20OST_%E4%BD%A0%E5%BE%AE%E7%AC%91%E6%97%B6%E5%BE%88%E7%BE%8E_%E4%B8%BB%E9%A2%98%E6%9B%B2).mp4', // GANTI CDN DISINI
      deskripsi:
        'enampilan memukau dengan tata cahaya panggung yang megah. Menyoroti kualitas vokal yang jernih, tinggi, dan kuat dalam balutan aransemen musik yang epik.',
    },
  ]
  daftarVideo.value = dataVideoNyata
})

// ================= FUNGSI OPERASIONAL: AUDIO PLAYER & TIMELINE =================

// Dipanggil saat salah satu card lagu diklik di Home atau Antrean
const bukaDetailLagu = (song) => {
  laguTerpilih.value = song
  halamanAktif.value = 'songDetail'
  nextTick(() => {
    if (audioRef.value) {
      // Terapkan volume yang sedang tersimpan di state saat ini
      audioRef.value.volume = volumeLevel.value
      audioRef.value.play()
      isPlaying.value = true
    }
  })
}

// Menjalankan atau menjeda musik
const togglePlay = () => {
  if (!audioRef.value) return
  if (isPlaying.value) {
    audioRef.value.pause()
    isPlaying.value = false
  } else {
    audioRef.value.play()
    isPlaying.value = true
  }
}

// BARU: Otomatis dipanggil tag <audio> setiap detiknya berubah
const updateWaktuLagu = () => {
  if (audioRef.value) {
    waktuBerjalan.value = Math.floor(audioRef.value.currentTime)
  }
}

// BARU: Otomatis dipanggil saat metadata file lagu selesai dibaca browser
const loadDurasiLagu = () => {
  if (audioRef.value) {
    durasiTotal.value = Math.floor(audioRef.value.duration)
  }
}

// BARU: Mengubah durasi musik secara manual saat slider timeline ditarik user
const geserDurasiLagu = () => {
  if (audioRef.value) {
    audioRef.value.currentTime = waktuBerjalan.value
  }
}

// BARU: Helper untuk mengubah angka detik murni menjadi format menit:detik ramah user
const konversiMenitDetik = (detikMurni) => {
  if (isNaN(detikMurni)) return '0:00'
  const menit = Math.floor(detikMurni / 60)
  const sisaDetik = Math.floor(detikMurni % 60)
  // Menambahkan angka 0 di depan sisaDetik jika angkanya di bawah 10
  return `${menit}:${sisaDetik < 10 ? '0' : ''}${sisaDetik}`
}

// Mengubah tingkat kekerasan suara
const aturVolume = () => {
  if (audioRef.value) {
    const vol = parseFloat(volumeLevel.value)
    audioRef.value.volume = vol
  }
}

// Navigasi ke lagu selanjutnya
const nextLagu = () => {
  const currentIndex = daftarLagu.value.findIndex((l) => l.id === laguTerpilih.value.id)
  if (currentIndex < daftarLagu.value.length - 1) {
    bukaDetailLagu(daftarLagu.value[currentIndex + 1])
  } else {
    bukaDetailLagu(daftarLagu.value[0]) // Siklus melingkar kembali ke lagu nomor 1
  }
}

// Navigasi ke lagu sebelumnya
const prevLagu = () => {
  const currentIndex = daftarLagu.value.findIndex((l) => l.id === laguTerpilih.value.id)
  if (currentIndex > 0) {
    bukaDetailLagu(daftarLagu.value[currentIndex - 1])
  } else {
    bukaDetailLagu(daftarLagu.value[daftarLagu.value.length - 1]) // Lompat ke lagu paling belakang
  }
}

// ================= FUNGSI OPERASIONAL: MODE FULLSCREEN (TETAP SAMA) =================
const bukaFullScreen = () => {
  isFullScreen.value = true
  zoomLevel.value = 1
}

const tutupFullScreen = () => {
  isFullScreen.value = false
}

const zoomIn = () => {
  if (zoomLevel.value < 3) zoomLevel.value += 0.2
}

const zoomOut = () => {
  if (zoomLevel.value > 0.4) zoomLevel.value -= 0.2
}

// ================= FUNGSI OPERASIONAL: PROFILE UPLOAD & LOCAL STORAGE (TETAP SAMA) =================
const handleUploadFoto = (event) => {
  const file = event.target.files[0]
  if (!file) return

  // 1. Nyalakan status loading saat file mulai diproses
  isUploadingProfile.value = true

  const reader = new FileReader()

  reader.onload = (e) => {
    const img = new Image()
    img.onload = () => {
      // 2. Proses Resize Gambar (Agar tidak melebihi 1MB)
      const canvas = document.createElement('canvas')
      let width = img.width
      let height = img.height

      const MAX_LEBAR_TINGGI = 400
      if (width > MAX_LEBAR_TINGGI || height > MAX_LEBAR_TINGGI) {
        if (width > height) {
          height *= MAX_LEBAR_TINGGI / width
          width = MAX_LEBAR_TINGGI
        } else {
          width *= MAX_LEBAR_TINGGI / height
          height = MAX_LEBAR_TINGGI
        }
      }

      canvas.width = width
      canvas.height = height
      const ctx = canvas.getContext('2d')
      ctx.drawImage(img, 0, 0, width, height)

      // 3. Konversi gambar kembali menjadi Blob lalu Base64
      canvas.toBlob(
        (blob) => {
          if (blob) {
            fotoProfil.value = URL.createObjectURL(blob)

            const readerBlob = new FileReader()
            readerBlob.onloadend = () => {
              // Simpan ke local storage
              localStorage.setItem('spojedy_foto_base64', readerBlob.result)

              // 4. Matikan status loading dengan jeda waktu buatan 1 detik
              setTimeout(() => {
                isUploadingProfile.value = false
              }, 1000)
            }
            readerBlob.readAsDataURL(blob)
          } else {
            // Pengaman: Jika proses blob gagal, matikan loading
            isUploadingProfile.value = false
          }
        },
        'image/jpeg',
        0.7, // Kualitas kompresi 70%
      )
    }

    // Pengaman: Jika file gambar rusak, matikan loading
    img.onerror = () => {
      isUploadingProfile.value = false
      alert('Gagal memuat gambar. Pastikan file yang diunggah valid.')
    }
    img.src = e.target.result
  }

  // Pengaman: Jika file gagal dibaca oleh browser, matikan loading
  reader.onerror = () => {
    isUploadingProfile.value = false
    alert('Gagal membaca file.')
  }

  reader.readAsDataURL(file)
}

const simpanKeLocalStorage = () => {
  localStorage.setItem('spojedy_username', username.value)
  localStorage.setItem('spojedy_theme', isDarkMode.value.toString())
  alert('Profil berhasil disimpan ke Local Storage!')
}

// ================= STATE MUSIC VIDEO =================
const daftarVideo = ref([])
const videoTerpilih = ref(null)

const bukaDetailVideo = (vid) => {
  // Otomatis pause lagu jika sedang menyala agar suara tidak tabrakan
  if (audioRef.value && isPlaying.value) {
    togglePlay()
  }
  videoTerpilih.value = vid
  halamanAktif.value = 'mvDetail'
}

const nextVideo = () => {
  const currentIndex = daftarVideo.value.findIndex((v) => v.id === videoTerpilih.value.id)
  if (currentIndex < daftarVideo.value.length - 1) {
    bukaDetailVideo(daftarVideo.value[currentIndex + 1])
  } else {
    bukaDetailVideo(daftarVideo.value[0])
  }
}

const prevVideo = () => {
  const currentIndex = daftarVideo.value.findIndex((v) => v.id === videoTerpilih.value.id)
  if (currentIndex > 0) {
    bukaDetailVideo(daftarVideo.value[currentIndex - 1])
  } else {
    bukaDetailVideo(daftarVideo.value[daftarVideo.value.length - 1])
  }
}

const tontonMvLagu = () => {
  const videoSesuai =
    daftarVideo.value.find((vid) => vid.id === laguTerpilih.value?.id) || daftarVideo.value[0]
  bukaDetailVideo(videoSesuai)
}
</script>

<style>
/* Mengatur style track agar bisa menampilkan dua warna (orange & abu-abu) */
input[type='range'].duration-slider {
  -webkit-appearance: none;
  height: 6px;
  border-radius: 5px;
  background: var(--track-color); /* Kita akan mengontrol ini via JS */
  outline: none;
}

/* Styling thumb (bola oranye) agar tetap konsisten */
input[type='range'].duration-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #f97316; /* Oranye */
  cursor: pointer;
}
</style>
