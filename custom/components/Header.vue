<template>
  <div class="py-3 mx-3 lg:mx-auto max-w-6xl">
    <section class="bg-red-400 rounded-xl px-3 py-3 flex justify-between">
      <section class="logo">
        <a href="/" class="font-bold">Pocketstore.io - Plugins</a>
      </section>
      <nav class="desktop hidden lg:block">Test</nav>
      <nav class="mobile block lg:hidden">
        <button v-if="!open" @click="open = !open">
          <font-awesome-icon :icon="['fas', 'bars']"/>
        </button>
        <button v-else @click="open = !open">
          <font-awesome-icon :icon="['fas', 'times']"/>
        </button>
      </nav>
    </section>
    <section v-if="open" class="navigation mt-3 mobile lg:hidden bg-white rounded-xl px-3 py-3">
      <section class="grid grid-cols-6 gap-3">
        <div class="col-span-3 md:col-span-2">
          <a href="/de" class="btn btn-block btn-primary">
            <font-awesome-icon :icon="['fas', 'home']"/>
            <span>Startseite</span>
          </a>
        </div>
        <div class="col-span-3 md:col-span-2">
          <a href="/de/catalog" class="btn btn-block btn-primary">
            <font-awesome-icon :icon="['fas', 'magnifying-glass']"/>
            <span>Suche</span>
          </a>
        </div>
        <div class="col-span-3 md:col-span-2">
          <a href="/de/blog" class="btn btn-block btn-primary">
            <font-awesome-icon :icon="['fas', 'rss']"/>
            <span>Blog</span>
          </a>
        </div>
        <div class="col-span-3 md:col-span-2">
          <a href="/de/catalog" class="btn btn-block btn-primary">
            <font-awesome-icon :icon="['fas', 'list']"/>
            <span>Katalog</span>
          </a>
        </div>
      </section>
    </section>
  </div>
</template>

<script setup lang="ts">
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'
import {useLocalStorage} from '@vueuse/core'

const open = useLocalStorage('navigation', false)

onMounted(()=>{
  open.value = false;
})
</script>
