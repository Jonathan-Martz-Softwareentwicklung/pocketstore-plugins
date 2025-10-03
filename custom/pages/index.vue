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
      <div v-for="plugin in plugins" class="col-span-6 md:col-span-3">
        <div class="hero bg-gray-300 py-12">
          <div class="hero-content text-center">
            <div class="max-w-md">
              <h1 class="text-3xl font-bold">{{plugin.name}}</h1>
              <p class="py-6">
                {{plugin.description}}
              </p>
              <section class="actions space-x-3">
                <button class="btn btn-primary">View</button>
                <button class="btn btn-primary">Code</button>
              </section>
            </div>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
const plugins = ref([]);

const load = async () =>{
  let response = await fetch('https://download.pocketstore.io/modules');
  plugins.value = await response.json();
}

onMounted(()=>{
  load()
});
</script>