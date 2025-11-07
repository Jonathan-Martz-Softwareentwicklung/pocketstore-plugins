<template>
  <section class="grid grid-cols-6 gap-3">
    <div class="col-span-3 flex items-center mt-3"><label class="label font-bold text-sm">aktuelle Sprache</label></div>
    <div class="col-span-3">
      <select v-model="lang" class="select w-full mt-3" @change="change($event.target.value)">
        <option value="de">Deutsch</option>
        <option value="en">English</option>
      </select>
    </div>
  </section>
</template>
<script setup lang="ts">
import {useLocalStorage} from '@vueuse/core'

const lang = useLocalStorage('lang', 'de', {});
const {setLocale} = useI18n()

const change = (locale) => {
  setLocale(locale);
  lang.value = locale;
}

onMounted(() => {
  setLocale(lang.value);
});
</script>