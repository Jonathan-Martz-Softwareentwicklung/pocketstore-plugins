<template>
  <section class="bg-white px-3 py-3">
    <section class="grid grid-cols-6 gap-3">
      <div v-for="item in 9" class="col-span-6 md:col-span-2">
          <ArticelCard />
      </div>
    </section>
  </section>
</template>
<script setup lang="ts">
import ArticelCard from "@/components/blog/ArticelCard.vue";
import {usePocketBase} from "@/util/pocketbase";

const items = ref([]);

const pb = usePocketBase()

const load = async () =>{
  items.value = (await pb.collection('articels').getList(1,9)).items;
}

onMounted(load);
</script>