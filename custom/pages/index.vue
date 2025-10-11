<template>
  <section class="page bg-white px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div class="col-span-6">
        <h2 class="font-bold text-lg">Willkommen in unserem PocketStore für Plugins von PocketStore</h2>
        <p class="block text-left max-w-xl">
          Hier findest du alle Plugins wie die Kasse, den Katalog und alle andere Plugins.
          In Zukunft kommen auch custom plugins von anderen Herstellern.
        </p>
      </div>
      <div v-for="(plugin,index) in plugins" class="col-span-6 md:col-span-3">
        <HeroProduct :plugin="plugin" :index="index" />
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
import HeroProduct from "@/components/HeroProduct.vue";

const plugins = ref([]);

const load = async () => {
  let response = await fetch('https://download.pocketstore.io/plugins');
  plugins.value = await response.json();
  plugins.value.sort((a, b) => a.name.localeCompare(b.name))
}

onMounted(() => {
  load()
});
</script>