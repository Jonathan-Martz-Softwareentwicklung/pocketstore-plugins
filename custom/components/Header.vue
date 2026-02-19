<template>
  <header
      class="sticky top-0 z-50 mb-3 backdrop-blur bg-white/60 dark:bg-slate-900/60 border-b border-slate-200/60 dark:border-slate-800/60"
      @keydown.esc="closeAll"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <div class="flex items-center gap-4">
          <a href="/" class="flex items-center gap-3">
            <img src="https://picsum.photos/120" class="w-12 h-12" alt="">
            <div class="hidden sm:flex flex-col leading-tight">
              <span class="text-slate-900 dark:text-slate-100 font-semibold">PocketStore.io</span>
              <span class="text-xs text-slate-500 text-white">Plugins</span>
            </div>
          </a>
        </div>

        <!-- Middle: Navigation -->
        <nav class="hidden md:flex items-center gap-1">
          <a href="/marketplace"
             class="px-3 py-2 rounded-md text-slate-700 dark:text-slate-200 hover:bg-slate-100 dark:hover:bg-slate-800 transition">Marketplace</a>

          <!-- Plugins dropdown -->
          <div class="relative" @mouseenter="openPlugins = true" @mouseleave="openPlugins = false">
            <button
                class="flex items-center gap-2 px-3 py-2 rounded-md text-slate-700 dark:text-slate-200 hover:bg-slate-100 dark:hover:bg-slate-800 transition"
                :aria-expanded="openPlugins"
                @click.prevent="togglePlugins"
            >
              Plugins
              <font-awesome-icon :icon="['fas', 'chevron-down']" class="text-sm"/>
            </button>

            <transition name="fade-scale">
              <div
                  v-if="openPlugins"
                  class="absolute left-0 mt-2 w-96 bg-white dark:bg-slate-900 border border-slate-200/60 dark:border-slate-800/60 rounded-lg shadow-lg p-4"
                  role="menu"
              >
                <div class="flex items-center justify-between mb-3">
                  <strong class="text-slate-900 dark:text-slate-100">Popular Plugins</strong>
                  <a href="/plugins" class="text-xs text-indigo-600 hover:underline">View all</a>
                </div>

                <div class="grid grid-cols-2 gap-3">
                  <template v-for="item in featuredPlugins" :key="item.slug">
                    <a :href="item.href"
                       class="flex gap-3 items-start p-2 rounded-md hover:bg-slate-50 dark:hover:bg-slate-800 transition">
                      <div
                          class="flex-none w-10 h-10 rounded-md bg-slate-100 dark:bg-slate-800 flex items-center justify-center text-indigo-600">
                        <span class="text-sm font-semibold">{{ item.icon }}</span>
                      </div>
                      <div class="min-w-0">
                        <div class="flex items-center justify-between">
                          <p class="text-sm font-medium text-slate-900 dark:text-slate-100 truncate">{{ item.name }}</p>
                          <span v-if="item.badge"
                                class="ml-2 text-xs bg-indigo-100 text-indigo-700 px-2 py-0.5 rounded">{{
                              item.badge
                            }}</span>
                        </div>
                        <p class="mt-1 text-xs text-slate-500 dark:text-slate-400 truncate">{{ item.description }}</p>
                      </div>
                    </a>
                  </template>
                </div>
              </div>
            </transition>
          </div>

          <a href="/docs"
             class="px-3 py-2 rounded-md text-slate-700 dark:text-slate-200 hover:bg-slate-100 dark:hover:bg-slate-800 transition">Docs</a>
        </nav>

        <!-- Right: Actions -->
        <div class="flex items-center gap-3">
          <!-- Search (large screens) -->
          <div class="hidden md:flex items-center w-64">
            <div class="relative w-full">
              <input
                  v-model="query"
                  @keyup.enter="emitSearch"
                  type="search"
                  placeholder="Search plugins…"
                  class="w-full pl-3 pr-10 py-2 rounded-lg border border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 text-sm text-slate-700 dark:text-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-400"
                  aria-label="Search plugins"
              />
              <button @click="emitSearch"
                      class="absolute right-1 top-1/2 -translate-y-1/2 text-slate-500 hover:text-slate-700 dark:hover:text-slate-300 p-1">
                <font-awesome-icon :icon="['fas', 'magnifying-glass']" class="text-sm"/>
              </button>
            </div>
          </div>

          <button v-if="pb.authStore.isValid" @click="navigateTo('/customer?id='+pb.authStore.record.id)"
                  class="btn btn-neutral btn-sm">
            <font-awesome-icon :icon="['fas', 'user']" class="text-sm"/>
          </button>
          <button @click="openLanguageModal = true" class="btn btn-neutral btn-sm">
            <font-awesome-icon :icon="['fas', 'globe']" class="text-sm"/>
          </button>
          <!-- Login / Avatar -->
          <div class="hidden md:block">
            <button v-if="!pb.authStore.isValid" @click="navigateTo('/customer/login')" class="btn btn-success btn-sm">Login</button>
            <button v-else @click="navigateTo('/customer/logout')" class="btn btn-warning btn-sm">Logout</button>
          </div>
          <button @click="mobileOpen = !mobileOpen" class="md:hidden p-2 btn btn-neutral btn-sm">
            <font-awesome-icon v-if="!mobileOpen" :icon="['fas', 'bars']" class="text-xl"/>
            <font-awesome-icon v-else :icon="['fas', 'times']" class="text-xl"/>
          </button>
        </div>
      </div>
      <section v-if="mobileOpen" class="md:hidden mb-2 bg-white px-3 py-3">
        <section class="grid grid-cols-6 gap-3">
          <div class="col-span-3">
            <button @click="navigateTo('/');mobileOpen = false" class="btn btn-block">
              Startseite
            </button>
          </div>
          <div class="col-span-3">
            <button @click="navigateTo('/blog');mobileOpen = false" class="btn btn-block">
              Blog
            </button>
          </div>
          <div class="col-span-3">
            <button @click="navigateTo('/catalog');mobileOpen = false" class="btn btn-block">
              Katalog
            </button>
          </div>
          <div class="col-span-3">
            <button @click="navigateTo('/search');mobileOpen = false" class="btn btn-block">
              Suche
            </button>
          </div>
        </section>
      </section>
    </div>
  </header>

  <input type="checkbox" v-model="openLanguageModal" class="modal-toggle"/>
  <div class="modal" role="dialog">
    <div class="modal-box block text-center">
      <h3 class="text-lg font-bold">Sprache auswählen oder wechseln</h3>
      <section>
        <LanguageSwitcher></LanguageSwitcher>
      </section>
      <div class="modal-action">
        <label @click="openLanguageModal = false" class="btn">{{ $t('btn.close') }}</label>
      </div>
    </div>
    <form method="dialog" class="modal-backdrop">
      <button @click="openLanguageModal = false">close</button>
    </form>
  </div>
</template>

<script setup>
import {ref} from 'vue'
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import {usePocketBase} from "~/utils/pocketbase.ts";
import {useLocalStorage} from '@vueuse/core'
import LanguageSwitcher from "./LanguageSwitcher.vue";

const theme = useLocalStorage('theme', 'light', {});
const openLanguageModal = ref(false)
const mobileOpen = ref(false)
const mobilePluginsOpen = ref(false)
const openPlugins = ref(false)
const query = ref('')
const pb = usePocketBase();
const toggleDarkMode = () => {
  if (theme.value == 'light') {
    theme.value = 'dark'
  } else {
    theme.value = 'light'
  }
}


// example featured plugin data — replace with API or props
const featuredPlugins = ref([
  {
    slug: 'analytics',
    name: 'Analytics Pro',
    description: 'Advanced usage tracking',
    href: '/plugins/analytics-pro',
    badge: 'Popular',
    icon: 'A'
  },
  {
    slug: 'seo',
    name: 'SEO Booster',
    description: 'Improve search rankings',
    href: '/plugins/seo-booster',
    badge: null,
    icon: 'S'
  },
  {
    slug: 'payments',
    name: 'Payments',
    description: 'Fast checkout flow',
    href: '/plugins/payments',
    badge: 'New',
    icon: 'P'
  },
  {
    slug: 'chat',
    name: 'Live Chat',
    description: 'Real-time support widget',
    href: '/plugins/live-chat',
    badge: null,
    icon: 'C'
  }, {
    slug: 'chat',
    name: 'Live Chat',
    description: 'Real-time support widget',
    href: '/plugins/live-chat',
    badge: null,
    icon: 'C'
  }, {
    slug: 'chat',
    name: 'Live Chat',
    description: 'Real-time support widget',
    href: '/plugins/live-chat',
    badge: null,
    icon: 'C'
  },
])

function closeAll() {
  mobileOpen.value = false
  mobilePluginsOpen.value = false
  openPlugins.value = false
}

// search emit — replace with emits or router push as needed
function emitSearch() {
  // Example: navigate to search results or emit an event
  // For now we simply navigate to a search page with query param
  if (!query.value) return
  window.location.href = `/plugins/search?q=${encodeURIComponent(query.value)}`
}

// plugins dropdown toggle
function togglePlugins() {
  openPlugins.value = !openPlugins.value
}


</script>