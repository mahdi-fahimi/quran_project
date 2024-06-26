
<template>
  <div class="card flex justify-center mt-8">
    <Select v-model="selectedCountry"
            :options="countries"
            :filter="true"
            variant="filled"
            optionLabel="name"
            :placeholder="countries[0].name"
            class="w-full md:w-56">
<!--      <template #value="slotProps">-->
        <div v-if="slotProps.value" class="flex items-center">
          <div>{{ slotProps.value.name }}</div>
        </div>
        <span v-else>
          {{ slotProps.placeholder }}
        </span>
<!--      </template>-->
<!--      <template #option="slotProps">-->
        <div class="flex items-center">
          <div>{{ slotProps.option.name }}</div>
        </div>
<!--      </template>-->
    </Select>
  </div>
</template>

<script setup>
import { ref } from "vue";

import Select from 'primevue/select';

const selectedCountry = ref();
const countries = ref([
  { name: 'حمد', code: '01' },
  { name: 'بقره', code: '02' },
  { name: 'آل عمران', code: '03' },
  { name: 'نساء', code: '04' },
  { name: 'مائده', code: '05' },
  { name: 'انعام', code: '06' },
  { name: 'اعراف', code: '07' },
  { name: 'انفال', code: '08' },
  { name: 'توبه', code: '09' },
  { name: 'یونس', code: '10' }
]);
</script>
