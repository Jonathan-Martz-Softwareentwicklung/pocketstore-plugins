<template>
  <section class="alert alert-info flex mb-3 xl:mx-auto">
    <Fa :icon="faInfoCircle" class="text-white" />
    <p class="text-sm font-bold w-full text-center text-white">
      Dies ist die Storefront für Pocketstore.io - Plugins
    </p>
    <Fa :icon="faInfoCircle" class="text-white" />
  </section>
</template>

<script lang="ts" setup>
import { faInfoCircle } from "@fortawesome/free-solid-svg-icons";
</script>