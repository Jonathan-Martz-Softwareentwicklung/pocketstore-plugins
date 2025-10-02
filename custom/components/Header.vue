<template>
  <div class="py-3 px-3">
    <section class="bg-white rounded-xl px-3 py-3 flex justify-between">
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
    <section v-if="open" class="navigation mt-3 mobile md:hidden bg-white rounded-xl px-3 py-3">
      Navigation
    </section>
  </div>
</template>

<script setup lang="ts">
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'
import {useLocalStorage} from '@vueuse/core'
import {onMounted} from "../../storefront/.nuxt/imports";

const open = useLocalStorage('navigation', false)
onMounted(()=>{
  open.value = false;
})
</script>
